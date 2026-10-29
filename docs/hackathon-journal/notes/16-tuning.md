---
tags: [tuning, balance, skill-issue]
---
# Tuning

> [!NOTE]
> **Status**
> These were my tuning notes from Saturday night. **Spread, hitboxes and trails are live on `main`.** The movement and gun-damage "Try" columns were **suggestions that were never applied**. Magazines came later from Aditya's branch (pistol 12 / 1.25 s, shotgun 6 / 1.8 s, sniper 5 / 2.2 s; see [09 Weapons & Combat](09-weapons-and-combat.md)). Phone feel was later reworked by Ryan and Aditya ([07 Controls & Motion](07-controls-and-motion.md)), so the "Phone feel" numbers below are historical.

All numbers live in `apps/game/data/*.tres`. Edit them in the Inspector and re-run (F5/F6); edits don't hot-reload.
**Method:** change one thing at a time, then play a 1v1 against yourself on the keyboard.

**Goal:** fights should last long enough for the duo to *talk*. A ~1 s time-to-kill is too fast for two people coordinating one body.

## Current → suggested (not applied yet)
### Movement (`movement/default_movement.tres`)
| Setting | Now | Try | Why |
|---|---|---|---|
| ground_accel | 40 | 28 | softens jitter from shaky tilt |
| air_accel | 12 | 14 | a bit more air control |
| jump_velocity | 7.0 | 7.6 | same height (~1.55 m)… |
| gravity_scale | 1.6 | 1.9 | …but snappier (0.8 s airtime instead of 0.9 s) |

→ Players can jump onto anything up to about **1.5 m**. Tell the map teammate: 2 m crates = not jumpable, 1.1 m cover = jumpable.

### Guns (`weapons/*.tres`)
| Gun | Change | Result |
|---|---|---|
| Pistol | damage 22→17, interval 0.28→0.3, headshot 2.0→1.75 | 6 shots, ~1.5 s to kill (was ~1.1 s) |
| Shotgun | 11×9 → 10×10 pellets, spread 6→5, range 28→20 | 2 shots close, 1 at point blank; stays short-range |
| Sniper | damage 90→75, interval 1.4→1.5, unscoped spread 3→4, scope FOV 18→20 | 2 body shots / 1 headshot; no-scoping is a gamble |

Quick formula: time to kill = (shots needed − 1) × fire interval, where shots needed = 100 ÷ damage rounded up.

### Spread (in place since 19:45, in `weapons/*.tres` → Spread)
| Gun | Base | Moving add | Airborne add | Crouch × | Bloom / shot (max, recovery) | Pattern |
|---|---|---|---|---|---|---|
| Pistol | 0.6° | +1.5° | +4° | 0.7 | 0.35° (2.5°, 6°/s) | random |
| Shotgun | 6° | +1° | +2° | 0.85 | none | **ring** (1 center + 8) |
| Sniper | 3° unscoped / 0° scoped | **+6°** | **+10°** | 0.5 | none | random |

**Why the sniper's moving penalty is huge:** a scoped sniper is perfect *only if the mover stands still*. The gunner has to say "STOP!", so spread is a teamwork lever, not just a balance number. This is the first piece of my "stance" idea ([03 Whiteboard Brainstorm](03-whiteboard-brainstorm.md)); the airborne *damage* bonus isn't built yet.

### Hitboxes (`hitboxes/default_hitboxes.tres`)
| Zone | Size (m) | Center offset | Damage |
|---|---|---|---|
| Head | 0.54 × 0.36 × 0.5 | 0.08 above `Head` | gun's headshot × (pistol/sniper 2.0, shotgun 1.5) |
| Body | 0.84 × 0.62 × 0.56 | 1.22 up from `Torso` | × 1.0 |
| Legs | 0.62 × 0.92 × 0.48 | 0.46 up from `Legs` | × 0.75 |

Example: a pistol does 44 / 22 / 16.5 to head / body / legs.

### Trails (`weapons/*.tres` → Trail)
| Gun | Tracer width | Lifetime | Impact size |
|---|---|---|---|
| Pistol | 0.025 m | 0.07 s | 0.06 m |
| Shotgun | 0.018 m | 0.06 s | 0.05 m |
| Sniper | 0.05 m | 0.30 s | 0.12 m (long, visible line, so everyone sees where the sniper is) |

### Aim & match
- `scoped_multiplier` 0.35 → 0.28 (matches the scope zoom, so aim feels the same scoped and unscoped)
- `kill_limit` 10 → 5 for demos; `respawn_delay` 3.0 → 2.5

### Phone feel (tune on real phones)
- Mover max tilt 25° → try 18°
- Gunner sensitivity 2.0 → try up to 3.0 if turning around needs body-spinning
