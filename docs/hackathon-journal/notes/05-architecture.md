---
tags: [architecture, godot, networking, skill-issue]
---
# Architecture

## The whole system
```
             ┌─────────── skillissue.vodka (Next.js on Vercel) ───────────┐
             │ /api/games       provision a game → returns wss://…/games/<id>│
             │ /api/connection  tells phones which relay to use             │
             │ /api/mvp         Gemini judges the match MVP                 │
             │ /api/mvp/badge   Gemini draws the MVP raccoon badge          │
             │ /api/leaderboard Tiger Data (Postgres) top 10 (site no longer shows it) │
             └───────────────▲─────────────────────────────▲──────────────┘
                             │ HTTPS                       │ HTTPS
  4 phones (Expo app) ──wss──► Node relay (apps/server) ◄──wss── Godot game on the TV
   Runner / Gunner              owns codes, slots, lobby         owns gameplay + stats
```
- **Phones never talk to Godot directly in production.** Both connect to the relay. The phone only needs the six-character code.
- **Dev fallback:** clear the control-plane setting and Godot hosts the lobby itself (`LobbyServer`, port 8080).
- **Data boundary** (from the whiteboard, and it held): **Tiger Data** = durable data (accounts, scores, stats, leaderboard). **WebSocket** = live input (movement, accel, gyro, tilt, button events). See [03 Whiteboard Brainstorm](03-whiteboard-brainstorm.md) Board 5.

## Monorepo
| Folder | What |
|---|---|
| `apps/game` | Godot 4.7.1 project (GL Compatibility renderer, Jolt physics) + embedded lobby server |
| `apps/companion` | Expo SDK 58 / React Native 0.88 phone controller, Practice, `/debug` tools |
| `apps/server` | Node WebSocket relay + integration tests (deployable on Render) |
| `apps/landing` | Next.js 16 App Router site and control plane (pnpm, Vercel) |
| `packages/protocol` | Shared message types (`events.ts`), protocol version 1 |
| `docs/` | network protocol, internet connection, Tiger Data, Android motion fix, gunner smoothing, fancy-UI report |

## Network protocol (summary of `docs/network-protocol.md`)
1. Game → `POST /api/games` → connects to `wss://…/games/<gameId>` → sends `hello {clientType:"game"}` → gets `game_registered` with a **6-character code** (alphabet without look-alikes: no I, L, O, 0, 1).
2. Phone → `GET /api/connection` → relay → `join_game {pairingCode, name}` → `select_slot {teamId: 1|2, role: movement|aim}` → `set_ready`.
3. Server broadcasts `lobby_state` (authoritative `assignments`, `players`, `minPlayers`). All slots ready → **3-second countdown** → `start_game` → `playing`.
4. Host sends `match_status` about once a second (scores, time left, kill target). At 10 kills or 5 minutes → `end_game {winningTeam, reason: kills|time|host}` → phones get `match_ended`.
5. **Play Again** → `reset_lobby` (same code and slots). Host disconnect closes the lobby; if the game loses its session mid-match, it clears the match and opens a fresh lobby.
6. Deadlines: phone join **10 s**, Godot connect **6 s** with backoff.

## Inside the game
### Scene layout
```
Main (main.tscn, Kenneth)
├── Match            rules (my duo_sandbox.gd grew into the real match mode)
├── World
│   ├── Map          The Pit (default) / Arena v2 / Brian's arena_box
│   └── Entities     Duos spawn here
├── Screens          TeamAView (left, Blue) | TeamBView (right, Red), each a SubViewport + Camera3D
└── HUD              CanvasLayer (Aditya's gameplay HUD + my scope overlay)
```
Both SubViewports render the same 3D world. Each camera follows its Duo's head.

### The Duo (my part)
```
Duo (CharacterBody3D)
├── Legs          ← Runner (walk direction, leg animation)
├── Torso         ← Gunner (turn)
│   └── Head      ← Gunner (pitch), camera mount, guns, fedora
├── Components    Movement · Aim · Weapons · Health · Team · Hitbox
├── Fx            hat pop, death split, spawn shimmer (duo_fx.gd)
└── Controllers   Phone / Keyboard (added at runtime)
```
**The key idea: input is decoupled.**
- `DuoInput` is one frame of intent (move, jump, crouch, sprint, aim delta, fire, scope, gun slot).
- Every `DuoController` *adds* its part each frame, so phones, keyboard or a future bot can drive the same Duo.
- Components only read `DuoInput` and never know where it came from.
- **Why:** we could test full 2v2 matches at a desk with no phones and no four people.

| Component | Does |
|---|---|
| Movement | velocity, gravity, jump buffer, crouch (won't stand up under a ceiling), sprint, aim-relative or tank forward |
| Aim | Torso yaw + Head pitch, slower while scoped |
| Weapons | pistol/shotgun/sniper, hitscan, spread + bloom, magazines, pickups, scope, first- and third-person models |
| Health | HP, damage, spawn protection, `heal()` (medkits), `damaged`/`died` signals |
| Team | team color tint (darker trim color), render layers, hit flash, spawn shimmer |
| Hitbox | sizes Head/Body/Legs hurtboxes from a `HitboxProfile` resource |

### Rules that keep it reusable
- **Signals go up, never sideways:** `Health.died` → `Duo` → `GameEvents.duo_killed` → mode and HUD listen.
- **Tuning lives in Resources (`.tres`):** a new gun is a new data file, not new code ([16 Tuning](16-tuning.md)).
- **Render layers do "don't see yourself":** each team's camera hides its own body and gun but sees the enemy's.
- **Map ≠ mode ≠ character:** new map = new scene; new mode = new script; new input = new controller.

### Autoloads
`GameEvents` (signal bus: health, score, kills, match end), `NetworkClient`, `GameSession`, `InputRouter` (Kenneth), `MatchStats`, `MvpService` (Ryan), plus SFX on the `powerups` branch.

> [!NOTE]
> **Why I dropped my own globals (Sat 18:18)**
> I had written my own `GameEvents` / `NetworkBridge` / `PlayerRegistry`. Kenneth pushed his with **the same names but different signals**. He owns the structure, so his became the source of truth: I deleted mine and adapted. Result: PR #1 changed **zero** existing files.

## History of the networking design
| When | Version |
|---|---|
| Sat 16:06–16:35 | My standalone prototype: zero-dependency Node relay + **web** phone controller (`move`, `aim`, `btn`, `weapon` JSON) |
| Sat 17:00–18:30 | Team chose a **native Expo app** (no HTTPS needed for motion sensors) |
| Sat 19:36–19:49 | Ryan's WebSocket server + Kenneth's Godot networking layer; `InputRouter` feeds phones into my `PhoneDuoController` |
| Sun 01:24 | Godot **hosts the lobby server itself** |
| Sun 04:02 | **Online control plane** + landing app: game provisions through skillissue.vodka |
| Sun 05:28–06:01 | Join-by-code through the relay only; join diagnostics; fix for phones never sending the join (React Native `bufferedAmount`) |
