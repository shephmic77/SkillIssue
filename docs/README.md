# Documentation

## Start here

| Doc | What it covers |
| --- | --- |
| [Setup, controls and development](setup-and-development.md) | Running the game and phone app, the full control scheme, graphics settings, the MVP judge, tests |
| [Network protocol](network-protocol.md) | How the game, phones and relay connect, and every message they send |
| [Online play setup](online-play-setup.md) | Running the relay on the internet behind TLS |
| [Leaderboard database](leaderboard-database.md) | The Tiger Data (Postgres) leaderboard table and how the website reads it |

## Project history

| Folder | What's inside |
| --- | --- |
| [hackathon-journal/](hackathon-journal/README.md) | Michael's notebook from HackPSU Fall 2026: idea, whiteboards, team roles, every system, decision log, timeline, testing log, retrospective, and the DEV post draft. 21 notes and about 40 images |
| [website/](website/README.md) | A permanent snapshot of skillissue.vodka: full-page screenshots, artwork, and how to open the offline copy |
| [dev-notes/](dev-notes/) | Reports written while building: [Android motion fix](dev-notes/android-motion-fix.md), [gunner aim smoothing](dev-notes/gunner-aim-smoothing.md), [UI overhaul](dev-notes/ui-overhaul-report.md) |
| [screenshots/](screenshots/) | Screenshots from before the noir theme: gameplay HUD, graphics menu, phone practice mode |

## Per-app docs

- [Game (`apps/game`)](../apps/game/README.md), with deeper docs for the [Duo character](../apps/game/entities/duo/README.md), [prototypes](../apps/game/prototypes/README.md), [music](../apps/game/audio/music/README.md) and [audio credits](../apps/game/audio/CREDITS.md)
- [Phone app (`apps/companion`)](../apps/companion/README.md)
- [Website (`apps/landing`)](../apps/landing/README.md)
- [Relay server (`apps/server`)](../apps/server/README.md)
- [Shared protocol (`packages/protocol`)](../packages/protocol/README.md)

## File names changed in this fork

To make the layout easier to follow, some files were moved or renamed. Nothing was deleted except one byte-identical editor temp file (`main.tscn2604731255.tmp`). Every `res://` path, autoload, test and import file was updated, and the Godot smoke tests pass before and after (gameplay 71, lifecycle 25, rules 32 checks).

The [hackathon journal](hackathon-journal/README.md) is a record from the weekend, so it keeps the **old** names. Use this table to translate.

### Game (`apps/game`)

| Old name | New name | Why |
| --- | --- | --- |
| `modes/duo_sandbox.tscn` / `.gd` | `modes/match.tscn` / `.gd` | It's the real match everyone plays, not a sandbox |
| `main.tscn` | `modes/split_screen_layout.tscn` | The split-screen viewports and HUD layout the match builds on |
| `match.gd` | `modes/match_placeholder.gd` | An empty starter script on the layout's `Match` node |
| `arena_box.tscn` | `maps/arena_base.tscn` | Brian's original arena; the base Arena v2 builds on |
| `item_pickup.gd` | `entities/pickups/health_pickup.gd` | It's the health pickup |
| `game_events.gd` | `scripts/game_events.gd` | Autoload, kept with the other autoloads |
| `team_hud.gd` / `.tscn`, `crosshair.gd` | `ui/team_hud.*`, `ui/crosshair.gd` | UI files belong in `ui/` |
| `bigcovercolor.tres` | `materials/cover_block.tres` | Materials grouped and named for what they color |
| `wallcolor.tres` | `materials/wall.tres` | |
| `healthpickup.tres` | `materials/health_pickup.tres` | |
| `shotgunpickupcolor.tres` | `materials/shotgun_pickup.tres` | |
| `sniperpickupcolor.tres` | `materials/sniper_pickup.tres` | |
| `spawnpoint_color.tres` | `materials/spawn_point.tres` | |
| `box.tres` | `prototypes/box_collision_shape.tres` | An unused collision shape, not a material |
| `PlayerMovement.gd`, `PlayerHealthArmor.gd`, `weapon_system.gd`, `armor_pickup_object.gd` | `prototypes/player_movement.gd`, `player_health_armor.gd`, `weapon_system.gd`, `armor_pickup.gd` | Brian's first prototype, kept as history |
| `node_3d.tscn` | `prototypes/prototype_test_level.tscn` | Brian's first test level |
| `audio/9mm Single.wav`, `audio/20 Gauge Single.wav` | `audio/weapons/pistol_shot.wav`, `shotgun_shot.wav` | No spaces; grouped by use |
| `audio/GUI_Sound_Effects_by_Lokif/` | `audio/ui/` | Credit moved to [`audio/CREDITS.md`](../apps/game/audio/CREDITS.md) |
| `audio/ambient/Week 27 - Dusty Memories.ogg` (and others) | `audio/music/menu_dusty_memories.ogg`, `match_crushing_it.ogg`, `results_schmoovin.ogg`, `extra_batteries_not_included.ogg` | Named for where each track plays; original titles in the credits |

### Docs and repo

| Old name | New name |
| --- | --- |
| `README.md` (full guide) | [`docs/setup-and-development.md`](setup-and-development.md); the README is now a project overview |
| `docs/internet-connection.md` | [`docs/online-play-setup.md`](online-play-setup.md) |
| `docs/tiger-data.md` | [`docs/leaderboard-database.md`](leaderboard-database.md) |
| `docs/fancy-ui-report.md` | [`docs/dev-notes/ui-overhaul-report.md`](dev-notes/ui-overhaul-report.md) |
| `docs/gunner-smoothing-report.md` | [`docs/dev-notes/gunner-aim-smoothing.md`](dev-notes/gunner-aim-smoothing.md) |
| `docs/android-motion-fix.md` | [`docs/dev-notes/android-motion-fix.md`](dev-notes/android-motion-fix.md) |
| `docs/previews/` | [`docs/screenshots/`](screenshots/) |
| Unused Expo and Next.js starter images, `apps/companion/scripts/reset-project.js` | [`archive/starter-templates/`](../archive/README.md) |

Names that frameworks require stayed as they were: Next.js `page.tsx`, `layout.tsx` and `route.ts`; Expo Router `_layout.tsx` and `join.tsx` (which also serves the `skillissue://join` links); and Godot's `project.godot` and `default_bus_layout.tres`.
