---
tags: [decisions, skill-issue]
---
# Decision Log

Every key decision, who made it, and why. "Me" = Michael. Decisions #1–#58 were logged live on Saturday night and early Sunday; #59 onward were added from Sunday's work. Strikethrough or *status* notes mark decisions that were later reversed or didn't land on `main`.

| # | Decision | By | Why | Alternatives considered |
|---|---|---|---|---|
| 1 | Take the **Mystery Stack** route | Team | Creative constraints; judged on creativity + function | Open track |
| 2 | **2v2 duo shooter**, Screencheat/Quake style | Me / team | Rivalry + 4 players built in; fun on one TV | — |
| 3 | **Split one body between two players**: legs vs upper body | Me | Forces communication, so all three cards drive the gameplay | Each player controls their own character |
| 4 | **Motion as the main input** (tilt to walk, gyro to aim), not touch joysticks | Me | The phone-motion card requires motion as a *core* input; joysticks would fail it | Touch joysticks (first mockup) |
| 5 | Jump and crouch as **buttons for now**; shake/sprint/slide later | Me | Reliable first; motion gestures added once the core feels good | Shake/flick to jump (teammate's doc) |
| 6 | **3 guns**: pistol start, shotgun + sniper as floating pickups; scope sniper-only | Me | Quake-style map control; the sniper needs the mover to stand still | More guns, ammo |
| 7 | **Godot 4**, component-based Duo, controller interface, separate map and mode | Teammate's architecture doc | Reusable across maps and modes; keyboard testing without 4 phones | One big player script |
| 8 | **Native companion app** (Expo) for phones | Team | Native sensor access; no HTTPS problem | Web page controller (my prototype) |
| 9 | Work split: structure / map / **player (me)** | Team | Avoids `.tscn` merge conflicts | Everyone edits everything |
| 10 | Add my code as **new folders + a test scene**; don't edit teammates' files | Me | Zero overlap; teammates review before anything is wired in | Overwrite `main.tscn` |
| 11 | `pull.rebase true`, feature branch, pull request | Team / me | Clean history, review before merge | Merging straight into `main` |
| 12 | Claude makes **no changes without my permission**; I push manually | Me | I stay in control of the team repo | Claude pushes directly |
| 13 | **Crude geometry, function first**; mech-with-two-cats theme later | Me | Readability matters more than looks during a 1-day hackathon | Model the mech now |
| 14 | Player model priorities: separate legs/top, visible enemy gun, hit flash, matching hitboxes | Me | Each one makes the duo's state readable to both teams | Purely cosmetic detail |
| 15 | **Use the teammate's global scripts** and drop mine | Me | They own the structure; same names, different signals. Avoids two sources of truth | Keep mine and ask them to switch |
| 16 | Make the sandbox work with the real map **at runtime** (collision, light, spawns) instead of editing the map | Me | The map is the map teammate's file; flag "Use Collision" for them to tick | Edit `arena_box.tscn` myself |
| 17 | Don't pick between `weapon_system.gd` and `WeaponComponent` alone; raise it in the PR | Me | Overlapping work needs a team decision | Delete or replace theirs |
| 18 | Ship as **PR #1** for review instead of merging myself | Me | A teammate checks before it lands on `main` | Merge directly |
| 19 | **Merge PR #1 myself** after a team heads-up | Me | Low risk: only new folders, no conflicts, easy to revert; hackathon speed | Wait for a formal review |
| 20 | Character theme: **two raccoons in one trench coat** (replaces two-cat mech) | Me | The "two in a coat" joke *is* the split-body mechanic; instantly readable; two tails show it's two | Mech with two cat pilots |
| 21 | Concept style: **low-poly, light mafia/burglar** (fedora, squint, toothpick), team color on coat + fedora | Me | Cheap to model from primitives; matches the existing team-tint system | Detailed or realistic models |
| 22 | Commit with the GitHub **no-reply email** going forward | Me | "Keep email private" is on; the PSU email shows in public history | Keep the PSU email |
| 23 | Hitboxes = **3 data-driven boxes** (head/body/legs) in one `HitboxProfile` | Me | Simple to tune as the model changes; no code edits | Mesh-accurate hitboxes, hand-placed shapes in the scene |
| 24 | **Legs take ×0.75**, head uses each gun's headshot multiplier | Me | Rewards aim without a separate number per zone per gun | One multiplier table per gun |
| 25 | Spread reacts to the mover (walk / air / crouch) + optional **bloom** | Me | Turns accuracy into a mover↔gunner conversation; first step of the stance idea | Fixed spread per gun |
| 26 | Sniper: **+6° moving, +10° airborne** | Me | "Stop so I can shoot" is the core teamwork moment | Small penalty |
| 27 | Shotgun uses a **fixed ring pattern** | Me | Predictable and fair, easy to tune and test | Random pellets |
| 28 | F3 debug shows only the **enemy's** boxes on each screen | Me | Own boxes wrap the camera and tint everything | Show everything everywhere |
| 29 | Delete `duo-components` after confirming it's fully merged | Me | Keeps the repo tidy; nothing lost | Keep stale branches |
| 30 | *(ammo reversed by #40 / Aditya's magazines)* **Health only, no armor** for now; no ammo or reload yet | Me | Keep the Duo simple while hitboxes/spread land | Add armor/ammo to match Brian's pickups now |
| 31 | Rebuild hitboxes on the new `main` with a 3-way merge | Me | Keep teammates' sprint edits instead of overwriting them | Install the old zip |
| 32 | **Gun models as small scenes** (`entities/weapons/models/*.tscn`) referenced from each gun's data; one model is used in first person, on the enemy-visible Duo, and on the pickup | Me | Edit a gun's look in the Godot editor without code; one source of truth per gun | Separate meshes per use, hard-coded boxes |
| 33 | **Reuse the map's gun spots** (Brian's `SniperSpawnObject`, `ShotgunSpawnObject*`) and turn them into floating pickups at runtime | Me | Brian keeps owning the map layout; no edits to his file | Add my own pickup nodes into the map |
| 34 | **Sniper scope glint** visible to the enemy while scoped | Me | Scoping is powerful, so give the other team a fair warning; fits "stand still and snipe" | No tell |
| 35 | Scope overlay as its **own node** instead of more HUD code in the match mode | Me | Aditya's open branch rewrites that HUD code; a separate node merges cleanly with it | Edit the HUD builder directly |
| 36 | Opening in the coat is a **diamond** (flaps parting, folded-back edges, paws holding it open), not a rectangular window | Me | Reads as a real trench coat pulled apart, not a cut-out | Square window (first concept) |
| 37 | Raccoon model built from **primitives inside `duo.tscn`**, same node names the animator/hitboxes use | Me | Function first: no art pipeline, keeps leg animation, team tint and hitboxes working | Imported Blender model |
| 38 | **Head hitbox grows to cover the fedora** | Me | The concept says the fedora is the headshot zone; hats sticking out of the hitbox would feel unfair | Keep the old head box |
| 39 | **Simpler keyboard**: one "swap gun" key instead of 3 slot keys, no reload key (automatic), no overlapping keys between teams | Me | Testing on one laptop should be easy to explain in one line per team | Keep every phone button on its own key |
| 40 | **Pickup guns vanish when empty** (shotgun 6 shells, sniper 5 rounds); the pistol keeps reloading forever; a pickup tops up a gun you already hold | Me | Quake-style map control: you have to go back for the power weapons | Reloadable shotguns/snipers (Aditya's version) |
| 41 | **Low-poly, slim raccoon** (6-sided coat cones, faceted spheres, tapered sleeves/tails) closer to the mockup; hitboxes retuned to the slimmer shape | Me | Boxy model looked like a robot; faceted primitives give a "poly art" look with no art pipeline | Keep boxes, or model in Blender |
| 42 | **Arena v2 as a new scene that instances Brian's map unchanged** and adds on top; the match mode picks it with one setting | Me | Brian keeps owning the base layout (his edits still flow in); easy to switch back | Edit `arena_box.tscn` directly |
| 43 | **Three levels, Quake-style**: ground (0.5 m), decks (3.5 m), crow's nest (6 m). Center tower deck on pillars with open ground underneath, crow's nest on a column with the **sniper on top**; two side towers with a half-room under them; bridges deck-to-deck with open ground below | Me | Vertical fights and flanking routes; every structure has a space above *and* below | One raised platform (first v2) |
| 44 | Layout is **point-symmetric**: Blue's ramps start in the +z half, Red's in the -z half, side tower ramps alternate | Me | Each team gets equal routes from its own side | Mirror only across x |
| 45 | Switch off the old test player and health/armor spheres at runtime | Me | They don't work with the Duo (health only, no armor decision) | Delete them from Brian's file |
| 46 | **"The Pit"**: a new, self-contained enclosed map (default): pit (0 m) / ring (3 m) / porches (6.5 m), stairs between levels, covered corridor under the east/west ring decks | Me | Matches the Quake/UT reference: layered levels, structure above and below, no falling off the edge | Keep stacking on Brian's open field |
| 47 | Stairs are **looks only**; a hidden ramp underneath is what you walk on | Me | Godot's CharacterBody can't climb steps; ramps feel the same and never snag | Real step collision + step-up code |
| 48 | Power positions: **sniper in the pit** (exposed from every level), **shotguns on each team's home porch** | Me | Risk/reward: the best gun is in the most dangerous spot | Sniper on the highest point (too strong) |
| 49 | **Plain gray palette** for now, one material per surface type so it can be themed later | Me (per request) | Readability first; theme later | Orange Quake-style sky (tried, too much) |
| 50 | **Diagonal spawns** (Blue NE corner, Red SW corner) in **roofed spawn rooms** with two doorways; spawn points tucked out of both doorway sightlines | Me | Stops spawn camping: tested that no spawn point can be seen from the pit, ring, porches or the other spawn | Open corner spawns |
| 51 | **Solid stairs** + hidden ramp; grid shader on map surfaces (1 m grid, walls darker than floors) + dark baseboards/corner posts; spawns face their doorway | Me (from my playtest) | Playtest: you could walk through staircases, and spawning facing a flat gray wall made it hard to tell where you were | Plain flat gray |
| 52 | **Spawn protection 2 s** after a death (not at kick-off); bullets do nothing, firing ends it early, coat shimmers | Me | Pairs with the spawn rooms; blocks only bullets so falling and scripted damage still work (and the team's tests stay green) | Full invulnerability |
| 53 | **Hat flies off on a headshot; on death the two raccoons tumble out of the coat** (short-lived physics copies on the world layer) | Me | The funniest, most readable demo moments; both screens see it | Death = just disappear |
| 54 | Dropped the kill feed and damage numbers | Me (changed my mind) | Aditya's HUD already has hit markers, damage flash and a kill banner | Build both |
| 55 | **Raccoon polish**: bandit mask (two slanted patches + bridge), white brows/blaze/chin, fluffy cheeks, bushy striped tails, snap-brim fedora with dents + feather, notched lapels, double-breasted buttons, epaulets, storm flap, cuffs, pockets, back vent, hem; a darker team color for trim | Me | Closer to the concept art; trim in a darker team color reads well at a distance | Keep the simple version |
| 56 | *(not on `main`)* **Fedora = one-hit helmet**: its own HAT hitbox zone; a hat hit does body damage (no headshot bonus) and knocks the hat off; then the head is exposed until respawn | Me | Turns the hat joke into a mechanic: you get one "free" save on a headshot | Hat is just cosmetic inside the head zone |
| 57 | *(not on `main`; medkits shipped instead, #78)* **Healing**: after 3 s without damage, heal 15 HP/s back to full (both tunable on HealthComponent) | Me | Rewards backing off to cover; keeps fights flowing without health pickups | Health pickups |
| 58 | Hat brim cleaned up: one smooth 12-sided brim instead of upturned side plates | Me (playtest feedback) | The side plates looked like rectangles stuck to the hat | Keep snap brim |

| 59 | **Film noir** for everything: gray city streets, black-and-white UI, red and blue as the only saturated colors | Michael | *"noir… grayer tone, like city streets, where the red and blue characters stand out more"*. It also matches the whiteboard's "monotone environment, distinct sides by color" | Colorful arena, Quake orange |
| 60 | Neutral gray/white, **not amber**, for the noir map | Michael (from his flat-noir references) | The first pass read as sepia; the references were cool gray with neon | Warm amber noir |
| 61 | **One surface shader** (`noir_surface.gdshader`) with a pattern uniform for concrete, asphalt, brick, metal, wood, windows | Me | No texture pipeline; consistent look; cheap (the whiteboard said "use shaders where possible for speed") | Imported textures per surface |
| 62 | Team signs in the world: **red HOTEL on Red's side, blue BAR & GRILL on Blue's**, team neon in spawn rooms | Me | You can tell which side you're on at a glance without painting big team-colored walls | Team-colored floors/walls |
| 63 | Scenery in a **`visual_only`** group that the match mode doesn't make solid | Me | Rain, signs, skyline and trim must never block movement or bullets | Hand-disable collision per node |
| 64 | Red spawn light energy **0.7** | Me (review) | The first value washed the whole room red | Keep 1.0+ |
| 65 | UI as **black-and-white film title cards**: brick wall, spotlight, grain, flicker, extruded titles, **Chorus script** flourishes | Michael (references) / me | Same world as the map; reads "1940s detective film" instantly | Gray flat UI (first pass) |
| 66 | **No doorway or silhouette** in the menu, just the brick wall | Michael | Cleaner; keeps the focus on the title and team cards | Keep the lit doorway |
| 67 | Tab scoreboard as a **"CASE FILE"** with a lamplight leader highlight | Me | Theme-consistent and easy to read | Plain table |
| 68 | Phone app uses the **same kit**; keep component names (`SlantButton`) even when the look changes | Me | Restyle without touching every screen that imports them; smaller diff for Ryan | Rename everything |
| 69 | All flicker/grain/animation **respects reduce-motion** | Me | Accessibility; flicker can bother people | Always animate |
| 70 | Rubber-hose cartoon raccoons **rejected and removed everywhere** | Michael | Didn't fit the serious noir tone | Iterate on them |
| 71 | Tell Michael when code-drawn art can't match a hand-inked reference, and give a generator prompt instead | Me | Honest about the medium's limit; saves time | Keep iterating on weak art |
| 72 | Website = **approved PNG art + transparent hotspots**, plus HTML panels below | Michael | Exact fidelity to the art he liked; fast | Rebuild it in CSS/Next.js (built, previewed, not chosen) |
| 73 | Ship the new homepage as **one rewrite in `next.config.ts` + one HTML file**, `page.tsx` untouched, old version tagged `site-before-preview` | Me | Reversible in one command; zero risk to `/api/*` | Replace `page.tsx` |
| 74 | Judge the homepage **live**: push, and swap back if it's bad | Michael | Faster than local Next.js setup on his PC; the Vercel preview + tag make it safe | Local preview first |
| 75 | **Remove standings** and every link to it, painting it out of the hero PNG | Michael (what) / me (how) | The leaderboard wasn't configured; a dead section looks broken | Leave an empty "No cases on file yet" |
| 76 | Website drops the leaderboard entirely and adds **The Arsenal** (weapons) before The Pit | Ryan | Show what's real and playable | Keep the leaderboard API on the page |
| 77 | **Gemini judges the MVP** and draws a badge, with an offline rule and "Judged offline" label | Ryan | AI sponsor tech in a way that adds to the end screen; never blocks the results | No MVP / hard-coded rule only |
| 78 | Healing via **medkits** on the map (Brian) rather than my regen | Team (what shipped) | Map control and pickups fit the Quake style | Regen (#57) |
| 79 | Delete every branch once it's in `main` | Michael | Keeps the repo readable for five people | Keep old branches |
| 80 | These notes follow an **evidence convention** (confirmed / proposed / unknown); no invented results | Michael (journal) | Honest writeup for the DEV post and portfolio | Fill gaps with guesses |

## Open questions (as of Sun 11:47)
- ~~Keep `WeaponComponent` or `weapon_system.gd`?~~ → `WeaponComponent` is the game's weapon system.
- ~~Fold armor into Health?~~ → No armor in the shipped game.
- **Re-add the HAT helmet rule?** It's a fun mechanic; check with the team first (#56).
- **Merge `powerups`?** Bounty, mystery power-ups, swap on death and music are on Kenneth's branch. Needs a team decision and a test pass.
- **Merge `claude/mlh-tracks`?** Auth0 sign-in and the Tiger Data upload. Needs Vercel env vars and a Tiger table ([20 MLH & Partner Tech](20-mlh-and-partner-tech.md)).
- **Forward direction:** aim-relative vs tank. Both exist in `Movement.forward_mode`.
- **Rejected poster artboard** on the Design canvas: delete or keep?
