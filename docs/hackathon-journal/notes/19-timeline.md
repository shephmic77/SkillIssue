---
tags: [timeline, skill-issue]
---
# Timeline: Sat Oct 24 → Sun Oct 25, 2026

All times Eastern. Rows marked *(team)* come from commit timestamps on `main`. The rest is my own work log. Sunday rows from **05:05 onward** were reconstructed from commits and PR merge times. Times for my Sunday-morning design rounds are approximate (marked ~).

## Saturday: team commits at a glance
| Time | *(team)* |
|---|---|
| 15:16 | Ryan: initial commit → monorepo (15:30) → Expo template (15:40) |
| 15:28 | Kenneth: Godot project folder |
| 15:59–16:33 | Brian: first map blockout, ramp, player model |
| 16:36–17:40 | Ryan: gyro/accelerometer motion test → rolling average (10 samples) |
| 17:11–18:01 | Kenneth: main scene, split-screen structure, global scripts |
| 17:58–18:25 | Aditya: motion sensing / motion logic |
| 18:19–19:45 | Brian: `arena_box` → spawns → lighting → weapon spawns |
| 18:58–19:16 | Kenneth: HUD (crosshair, health bar, kill counter), anchored to split screens |
| 19:36–19:49 | Ryan: WebSocket server; Kenneth: Godot networking layer |
| 21:21–22:04 | Brian: item pickups (health, armor, ammo) |
| 23:10–23:32 | Ryan: PRs #2, #3 (gesture spec, X/Y/Z rewrite) |

## Saturday → early Sunday: my log

| Time | What happened |
|---|---|
| ~15:58 | Drew Mystery Stack: Phone motion / Rivalry / 4+. Picked a 2v2 duo shooter (Screencheat/Quake-like). Flagged that the touch-joystick mockup fails the motion card. |
| 16:05 | Locked controls: mover tilts + jump/crouch buttons; gunner gyro + fire/scope/3 guns; floating Quake-style pickups |
| 16:06 | Teammate shared the Godot architecture plan (duo components, controller interface, map template, deathmatch, split screen) |
| 16:06–16:35 | Built and tested a standalone prototype: Godot project + zero-dependency relay + phone web controller. 19/19 tests; fixed Android Chrome permission bug |
| 16:40 | Planned priorities: de-risk real phones first, tune feel, plan the demo |
| 16:48 | Roles settled: structure / map / **me = player & gameplay** |
| 16:53 | Tuning pass planned (numbers in [16 Tuning](16-tuning.md)) |
| 16:57–17:19 | Mechanics brainstorm: my stance ideas (still = less damage, airborne = more damage, less accuracy) + many more |
| 17:21 | Shared the team repo + `pull.rebase true` |
| 17:22 | Set the rule: no changes without my permission |
| 17:23 | Reviewed the repo: Godot 4.7 game, Expo companion app, empty protocol package |
| 17:28–17:32 | Cloned the repo, made branch `duo-components`, copied my 5 folders in (nothing committed) |
| 17:39 | Theme idea: mech piloted by two cats → parked, crude geometry for now |
| 17:42–17:46 | Built the split-screen test (Team A left, Team B right) that loads the team's `main.tscn` unchanged. 16/16 in Godot 4.7.1 |
| 17:46 | Got a one-zip drop-in + PowerShell steps (everything except push) |
| 18:01–18:05 | Functional player model: split legs/top, leg animation, visible enemy gun, hit flash, matching hitboxes. 15/15 |
| 18:09 | Final package + push steps + these notes |
| 18:16 | `git fetch` showed 13 new teammate commits, including **global scripts with the same names as mine** and a health/armor script |
| 18:18 | Adapted my code to their `GameEvents`; dropped my `core` folder → zero edits to teammate files |
| 18:19 | Team rule noted: `git config pull.rebase true` for divergent-branch errors |
| 18:20 | Pulled again: the real map arrived (no collision yet) plus `weapon_system.gd` |
| 18:22 | v3: sandbox works on their real map at runtime; all checks pass on their newest commit |
| 18:24–18:46 | Installed v3 locally, installed Godot 4.7.1, ran the sandbox on my PC with no errors |
| 18:48–18:49 | Staged and committed 46 files on `duo-components` |
| 18:50 | Push failed (no credential helper) → set `credential.helper manager` → pushed |
| 18:53 | Opened **PR #1**: checks passed, no conflicts |
| 18:56–19:00 | Decided to merge myself after a heads-up; checked `main` again (4 new teammate commits, none touching my folders) |
| 19:01 | **Merged PR #1 into `main`** → `git checkout main` + `git pull` locally |
| 19:05–19:08 | Not in Contributors yet: GitHub cache (commits are credited to shephmic77). Noted the switch to the no-reply email |
| 19:15–19:20 | Character concept: **two raccoons in a red trench coat** (low-poly, fedora, shotgun); revised so the bottom raccoon and both tails are obvious |
| 19:21 | Break. Notes updated |
| 19:25 | Next feature: tunable **hitboxes, gun trails and spread** (simple, data-driven) |
| 19:30–19:40 | Built `HitboxProfile` + `HitboxComponent` (head/body/legs), spread modifiers + bloom + shotgun ring, data-driven tracers/impacts, F3 debug view |
| 19:35 | Found the **rotated map in the merged test scene** (accidental editor save) → fixed |
| 19:40 | Fixed the debug tint and the overlap with Kenneth's new HUD |
| 19:45 | All 59 checks pass on the team's latest `main`; drop-in zip ready (not pushed yet) |
| 19:45–23:43 | Nap. Teammates: server, Godot networking (phones → Duo), sprint, map + pickups |
| 23:45–23:50 | Reviewed the new commits; Ryan force-pushed `main` twice (no file changes); re-synced locally |
| 23:53 | Deleted the merged `duo-components` branch on GitHub |
| 23:55–00:00 | Decision: health only, no armor/ammo/reload. Rebuilt hitboxes/spread/trails on the new `main` (3-way merge, sprint kept); all suites pass |
| 00:40–00:45 | Installed v2 on branch `hitboxes-spread`; tested on my PC (F6 → F3): everything works |
| 00:54–00:56 | Reviewed `.tscn` diffs (only expected changes), committed `d832e00` (17 files) with my no-reply email, pushed `hitboxes-spread`. Verified 1 commit ahead of `main`; `main` moved again (Ryan's landscape phone controller + lobby, PRs #4–#5) but no overlap, merges cleanly |
| 00:58 | Opened and merged **PR #6** (`hitboxes-spread` → `main`, merge commit `12cefee`, 1 check passed) |
| 01:00 | Pulled `main`; deleted local `hitboxes-spread` |
| 02:10 | Teammates merged the **full game flow** (menus, lobby, match rules, results) on top of my work; my sandbox is now the match mode |
| 02:14 | Next feature: **floating weapon pickups, gun models (pistol/shotgun/sniper), weapon cycling, sniper scope** (player model stays boxy for now) |
| 02:15–02:35 | Built and tested it on the latest `main` (33 new checks + all older suites); also verified it merges cleanly with Aditya's open `codex/fancy-ui` branch |
| 02:24–02:36 | Raccoon trench-coat model in Godot (diamond coat opening); paused once to start the **MLH services setup** (Auth0, Tiger Data) while teammates got food |
| 02:40 | Paused the MLH setup until Ryan is back; `main` moved again (Aditya's HUD + ammo/reload merged) → rebuilt weapons + raccoon on the new `main` (3-way merge) |
| 02:52 | Caught a key clash (O = reload and next gun for Red) |
| 02:58–03:10 | Simpler keyboard, pickup guns vanish when empty, slim low-poly raccoon model; team smoke tests (58 + 25) and my suites pass |
| 03:27 | First weapons/model version had already gone to `main` as "minor changes"; the update landed on a local copy of Aditya's branch → moved it to `player-model-v2` → **PR #7 merged** |
| 03:31–03:45 | Map work: **Arena v2** (sniper tower, ramps, mid cover, side ledges, leftovers off); all suites + team smoke tests pass |
| 03:40–04:00 | Rebuilt Arena v2 as a multi-level map (towers, bridges, crow's nest, under-deck space); route tests: ramps, nest, bridge, under the deck all walkable |
| 03:46–04:05 | Built **The Pit** from the Quake/UT references: 3 levels, 8 staircases, under-deck corridors, more cover on the upper levels, gray palette; all route + regression tests pass |
| 03:56–04:15 | Diagonal spawn rooms (walls + roof + 2 doorways); sightline test: no spawn visible from any camping spot |
| 04:26–04:50 | Spawn protection, hat pop on headshots, death split; dropped kill feed / damage numbers; big raccoon polish pass. All tests pass on the newest `main` |
| 04:40–04:55 | Concept sheet v2: renders of the real in-game model (hero, turnaround, close-ups, hat pop, death split) added next to the original concept |

## Sunday morning
| Time | What happened |
|---|---|
| 00:26–00:42 | *(team)* Ryan: PRs #4–#5 (web debugger with live 3D view; landscape phone controller) |
| 01:17–01:24 | *(team)* Ryan: stale autoloads removed; **Godot hosts the lobby server** |
| 01:41–02:14 | *(team)* Aditya: `codex/fancy-ui` + hitboxes merged; HUD/motion/lobby recovery/graphics rework; host-only controls + branding |
| 04:02 | *(team)* Ryan: **online control plane + landing app** |
| 04:51–05:01 | *(team)* Ryan: README/deploy docs, HackPSU footer, empty-lobby timeout |
| **05:05** | **Me: `9fae05f`, The Pit, spawn rooms + protection, hat pop / death split, raccoon polish, Arena v2** |
| 05:28–06:01 | *(team)* Ryan: join by code via relay, join diagnostics, fix phones never sending the join |
| 06:11–06:37 | *(team)* Ryan: players-needed setting, readable phone lobby, animated app background, Player Count slider, score-dash fix, settings close on Apply |
| 07:06 | *(team)* Aditya: smoother motion |
| 07:27 | *(team)* Ryan: **gyro-only Gunner** with buttons, camera not inverted |
| ~07:30–09:00 | Me: aesthetics list (site, map, scoreboard, menu, end screen, lobby, app). Noir map v1 (too amber) → neutral gray + red/blue neon (*"Map is really good"*) → menus/lobby/results in B&W film style → doorway + silhouette removed → case-file scoreboard |
| **09:14–09:16** | **Me: PR #8 noir theme merged (`5083a1b`)** |
| 09:37 | *(team)* Ryan: end screen with winner reveal, five stats, **Gemini MVP** |
| ~09:20–09:45 | Me: Expo Go / iPhone help (SDK 54 vs 58); Node 24, npm.cmd, PATH fixes |
| 09:44 | *(team)* Brian: "looked at new code, will add back in health packs" |
| **09:59–10:00** | **Me: PR #9 phone app noir merged (`01974ba`)** |
| 10:16–10:33 | *(team)* Ryan: reworked phone movement (lower latency, no manual recalibration); MVP badges; no-MVP picture |
| 10:30–10:34 | *(team)* Brian: health system working again, more medkits |
| ~09:30–10:45 | Me: website hero art attempts (flat silhouettes → teal poster → ink); rubber-hose style rejected; website prompt for another chat; fixed that chat's redesign zip; restyled the lower panels of the PNG preview |
| 10:57–11:03 | *(team)* Ryan: noir in-match phone screens + Practice; Settings/server URL removed from the phone |
| 10:58 | Me: `59dd89e` homepage preview served at `/` (old site tagged `site-before-preview`) |
| **11:05** | **Me: PR #10 merged (`74994a7`)**, after one "couldn't merge" retry. *"ok worked"* |
| 11:12 | *(team)* Brian: medkits fixed |
| **11:17–11:18** | **Me: PR #11, standings removed (`ea29adb`)** |
| 11:20 | *(team)* Kenneth: SFX autoload + audio paths on `powerups` (not merged) |
| 11:23–11:28 | *(team)* Aditya: Android sensor fix, normalized units; lateral movement with smaller tilts. Ryan: EAS lockfile; **The Arsenal**, leaderboard dropped |
| ~11:30 | Me: synced with `main`, deleted merged branches (`remove-standings`, `claude/reworked-movement` flagged) |
| 11:45 | *(team)* Ryan: website lobby-code scramble |
| 11:47 | *(team)* Aditya: gunner camera smoothing → `main` @ `6d291fc` |
| 11:46–12:00 | Me: these notes (whiteboards, journal and everything above → one vault) |
