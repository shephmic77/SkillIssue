---
tags: [controls, motion, phone, skill-issue]
---
# Controls & Motion

## Current controls (README on `main`, Sun 11:47)
Hold the phone **sideways, screen toward you**, at a comfortable tilted angle. It calibrates itself in a moment, slowly follows your grip while you rest, and recalibrates if you change grip, so **Recenter** is rarely needed.

| Phone | Motion / button | Action |
|---|---|---|
| **Runner** | Gentle forward/back tilt; tip either end down | Walk and strafe |
| **Runner** | Twist ~30° like a steering wheel, then back to center | Toggle sprint |
| **Runner** | Quick flick away / toward you | Toggle crouch / jump or stand |
| **Gunner** | Turn the phone left/right/up/down | Camera follows (not inverted) |
| **Gunner** | Hold **FIRE** | Shoot |
| **Gunner** | Tap **AIM** | Aim down sights / sniper scope |
| **Gunner** | Tap **RELOAD** | Reload |
| **Gunner** | Tap **SWITCH** | Next owned weapon |

Wheel gestures rearm below 12° with a 350 ms debounce.

**Keyboard practice:** keys are in `apps/game/entities/duo/README.md`. `R` reloads Blue's gun and `O` reloads Red's. Tab = scoreboard. F3 = hitboxes + spread.

## How the controls evolved
| Stage | Runner | Gunner | Notes (from commit messages) |
|---|---|---|---|
| Whiteboard | W/A/S/D, jump, slide/crouch, sprint (joystick pad) | rotation = shoot/aim, 3 gun buttons, scope, fire | First sketch ([03 Whiteboard Brainstorm](03-whiteboard-brainstorm.md) Board 7) |
| First mockup | Touch joystick | Touch joystick | **Fails the motion card** |
| Sat 16:05, my prototype | **Tilt** like a marble maze + JUMP/CROUCH buttons | **Gyro rotation rate** + FIRE/SCOPE/3 gun buttons | Motion becomes core |
| Sat 19:45 | + sprint (Q/U on keyboard) | | Teammates' edit |
| Sun 01:41–02:14 (Aditya) | Motion rework, host-only controls | RELOAD added with magazines | `codex/fancy-ui` merged |
| Sun 07:27 (Ryan) | | **Gyro only** for aim, buttons for actions, camera **not inverted** | "Gunner aims with the gyro only, acts with buttons" |
| Sun 10:16 (Ryan) | **Lower latency, snappier tilts, no manual recalibration**, explicit motion permission | | `claude/reworked-movement` |
| Sun 11:23–11:28 (Aditya) | Android sensor fix, normalized units, **lateral movement with smaller tilts** | | "Fix Android sensor access, normalize motion units"; "lateral movement responsive with smaller tilts" |
| Sun 11:47 (Aditya) | | **Smoothed gunner camera**, unsent turns kept | `docs/gunner-smoothing-report.md` |

### My first prototype controller (Saturday, web page)
Before the native app existed, I built a phone **web** controller to prove the idea. These screenshots are from that prototype:

<img src="../images/phone-mover.png" alt="phone mover" width="420">
*Mover: tilt pad with JUMP and CROUCH.*

<img src="../images/phone-gunner.png" alt="phone gunner" width="420">
*Gunner: gun buttons (greyed out until picked up), SCOPE and a big FIRE.*

## Motion design notes
- **Runner = tilt like an analog stick.** Neutral comes from where the phone is held, a **dead zone** stops drift from shaky hands, and a **max tilt** sets full speed (25° at first; Aditya later made lateral movement respond to smaller tilts).
- **Gunner = rotation rate, not absolute angle** (how Splatoon does motion aim). Absolute angles drift and need a home pose; rotation rate always feels 1:1. Turning is measured around **real-world up**, so it works whether the phone is upright or flat.
- **Smoothing:** a **10-sample rolling average** (Ryan, Sat 17:23–17:40), matching the "n samples" array on the whiteboard.

## Gotchas found
- **Browsers only allow motion sensors on HTTPS.** This killed the web controller plan. The native Expo app avoids it, and its web build shows a "use the native app" message.
- **iOS reports gravity with the opposite sign to Android.** It's detected by platform.
- **Newer Android Chrome also has `requestPermission()`.** My first prototype treated that as iOS and would have stuck Android players at "Tap to start". Fixed by detecting iOS by user agent.
- **Android sensor access and units** needed a dedicated fix (Aditya, Sun 11:23; `docs/android-motion-fix.md`).
- **Test every phone model the team owns before a demo.** Real-phone results are **not recorded** in these notes.
