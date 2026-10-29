---
tags: [concept, design, pitch, skill-issue]
---
# Pitch & Concept

## The elevator pitch
**Two minds. One body. Zero excuses.**

A noir detective in a fedora and trench coat walks into the rain. It looks like one intimidating figure, but it's really **two raccoons stacked in one coat**, trying to pass as human. The **top** raccoon peers out of the collar, aims and shoots. The **bottom** raccoon peeks out where the coat parts and does all the walking. Put one of those on **Red** and one on **Blue**: four players, two characters, and nobody in full control of their own body.

### Short descriptions for reuse
- **One sentence:** A 2v2 shooter where each team is two raccoons in one trench coat, controlled by two players on two phones.
- **Two sentences:** One player moves and the other aims and shoots, but both share a character and a health bar. Work together in a rain-soaked noir arena, or become your own team's biggest obstacle.
- **Website copy:** *One body. Two players. One of you moves. One of you shoots. Nobody has the full picture.*

## Design pillars
1. **Forced cooperation:** each player has exactly half the controls.
2. **Social friction as fun:** mistimed jumps, "STOP, I have a shot!", frantic callouts.
3. **An instantly readable gag:** "two raccoons in a trench coat" explains the split-body controls before anyone says a word.
4. **Fast, competitive rounds:** first to 10 kills or best score at 5 minutes.
5. **Phone as controller:** motion is the main input, not a gimmick on top of buttons.

## Inspiration
- **Screencheat / Quake / Unreal Tournament:** arena shooting, guns floating over the floor, peeking at the other team's half of the screen, layered maps.
- **Couch co-op:** everyone in one room, one TV, yelling.

## The core idea: a split body
| | Runner (bottom raccoon) | Gunner (top raccoon) |
|---|---|---|
| Controls | **Legs**: walk, strafe, sprint, jump, crouch | **Upper body**: turn, look up/down, fire, aim, reload, switch |
| Motion | Tilt like a marble maze; twist like a wheel; flick | Turn the phone like a camera (gyroscope) |
| Sees | The same screen as the Gunner | The same screen as the Runner |
| Can't | Shoot | Move |

**Why split it this way:** the Gunner sees an enemy but can't walk to it, and the Runner can dodge but can't shoot. Talking *is* the gameplay, so all three Mystery Stack cards drive the core loop instead of sitting on top of it.

## How the concept evolved
| When | Version | What changed |
|---|---|---|
| Sat ~15:58 | Touch-joystick 2v2 mockup | Rejected: fails the motion card |
| Sat ~16:05 | Mover + Gunner, both on motion | Locked the split-body controls ([07 Controls & Motion](07-controls-and-motion.md)) |
| Sat 17:39 | Mech piloted by two cats | Parked; crude boxes for now |
| Sat 19:15 | **Two raccoons in one trench coat** | The joke *is* the mechanic ([08 Duo Character](08-duo-character.md)) |
| Sunday (exact time unknown) | "Mover/Gunner" renamed **Runner/Gunner** | Clearer names in the UI and README |
| Sun morning (merged 09:16) | **Film noir** setting | Rainy city map, black-and-white UI, red/blue accents ([14 Art Direction](14-art-direction.md)) |

Early concept sheet (two raccoons, low-poly, red coat):

<img src="../images/raccoon-duo-concept.png" alt="raccoon duo concept" width="360">

## Alternatives on the whiteboard before this
The whiteboards ([03 Whiteboard Brainstorm](03-whiteboard-brainstorm.md)) show what the team considered first:
- **"3-D coordinated phone motion control game"** with obstacle types (fixed, moving, attacking), forward W/A/S/D to dodge obstacles, and a sideways "special attack".
- **General Track: "AI Conversation Analyzer"**, a non-game backup idea.
- A **mech piloted by two players** as the first skin idea, then the **trench coat detective**.
