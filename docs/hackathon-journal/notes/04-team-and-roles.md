---
tags: [team, roles, skill-issue]
---
# Team & Roles

Roles below are **confirmed from the commit history on `main`** (non-merge commits as of Sun 11:47). Commit counts measure activity, not effort; some people made a few big commits and others many small ones.

| Person | GitHub | Non-merge commits | Owned |
|---|---|---|---|
| **Ryan Smith** | Ryan-M-Smith | 65 | Repo owner and monorepo; **companion app** (Expo): sensors, rolling average, motion service; **WebSocket server/relay** and protocol; landing site and **control plane** (`/api/games`, `/api/connection`); full game flow (menus, lobby, results); join fixes; end screen with **Gemini MVP**; MLH branch (Auth0, Tiger Data). Many of these came through `claude/*` branches. |
| **Brian Podolskiy** | Brian-Podolskiy | 16 | First **map** (`node_3d.tscn` → `arena_box.tscn`), early test player, health + armor script, `weapon_system.gd`, item pickups; on Sunday **"health system working again"** and **medkits** |
| **Aditya Pratap Singh** | Aditya-Pratap-Singh-17 | 9 | **Motion sensing** logic; `codex/fancy-ui` (gameplay HUD, graphics/pause menus, smoke tests, ammo + reload, host-only controls, branding); Sunday: smoother motion, **Android sensor fix**, **lateral tilt**, **gunner camera smoothing** |
| **Michael Shepherd (me)** | shephmic77 | 9 | The **Duo** player (components, controllers, model), **hitboxes / spread / trails**, **weapon pickups + gun models + scope**, **raccoon model**, **Arena v2 → The Pit**, spawn rooms + protection, hat pop + death split, **noir theme** (map + game UI), **noir phone app**, **website homepage swap + standings removal** |
| **Kenneth Tran** | trnKen1 | 8 | **Godot structure**: `main.tscn`, split-screen views, global scripts (`GameEvents`), **HUD** (crosshair, health bar, kill counter), networking layer (`NetworkClient`, `GameSession`, `InputRouter`); Sunday: `powerups` branch (bounty, mystery power-ups, swap on death, music crossfade, SFX autoload; **not merged**) |

## Why we split by area
Godot `.tscn` files conflict badly when two people edit the same one. Each person owning **their own folders and scenes** let five people work in parallel on one Godot project. PR #1 merged with zero conflicts even though four teammate commits landed while it was open.

## My contributions, by PR
| PR | What | Merged |
|---|---|---|
| #1 | Duo player: components, controllers, crude model, split-screen test scene (46 new files, 0 edited) | Sat 19:01 |
| #6 | Tunable hitboxes, spread, gun trails, F3 debug view | Sun 00:58 |
| ("minor changes" + #7) | Weapon pickups, gun models, scope, simpler keyboard, empty pickup guns vanish, slim low-poly raccoon | Sun 03:06 / 03:29 |
| direct commit `9fae05f` | The Pit, spawn rooms + protection, hat pop / death split, raccoon polish, Arena v2 | Sun 05:05 |
| #8 | Noir theme: rainy city map, B&W menus, lobby, end screen, case-file scoreboard | Sun 09:16 |
| #9 | Phone app noir theme | Sun 10:00 |
| #10 | Homepage swap (`/` → `home-preview.html`) | Sun 11:05 |
| #11 | Remove standings section and its links | Sun 11:18 |

Full detail: [15 Git Workflow & PR History](15-git-workflow-and-pr-history.md).

## Working agreement with Claude (my assistant)
These are my own rules, still in effect:
- *"never add or remove or anything without my permission and consent and knowledge of changes"*: Claude lists what would change before anything happens.
- *"do all except push to git"*: Claude builds, tests on copies, and hands me a zip plus PowerShell steps. **I run every git command myself.**
- *"remove branches once they are in main"*: after each merge we delete the branch locally and on GitHub.
- For UI files, Ryan said changes were fine. Other teammates' files are never edited without asking.
