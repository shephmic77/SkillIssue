---
title: "Skill Issue: Home"
aliases: [Skill Issue, Skill Issue HackPSU 2026, SkillIssue]
type: project-moc
status: "Playable build on main; website live; post-hackathon polish"
event: HackPSU Fall 2026
dates: 2026-10-24 → 2026-10-25
team_size: 5
repo: https://github.com/Ryan-M-Smith/SkillIssue
site: https://skillissue.vodka/
tags: [projects/skill-issue, hackathon, game-development, home]
---

> [!NOTE]
> **About this journal.** These are my notes from HackPSU Fall 2026 (Oct 24–25), kept in Obsidian during the weekend and added to this fork as-is. Only the link format changed so they render on GitHub. The folder still opens as an Obsidian vault.
> The notes use the file names from that weekend (`duo_sandbox.tscn`, `main.tscn`, `arena_box.tscn`, ...). This fork renamed some of them; see [file names changed in this fork](../README.md#file-names-changed-in-this-fork).

# Skill Issue

> [!NOTE]
> **One body. Two players. Zero excuses.**
> **Skill Issue** is a 2v2 split-screen shooter built by five people at **HackPSU Fall 2026**. Each team is one character, **two raccoons in a single trench coat**, driven by **two phones**. The **Runner** (the bottom raccoon) tilts and flicks one phone to move. The **Gunner** (the top raccoon) turns the other phone to aim and taps to shoot. They share one body and one health bar. Neither can win alone.

![noir play](images/noir-play.png)
*The noir version of The Pit in a split-screen match, Blue on the left and Red on the right (rendered from `main`).*

| | |
|---|---|
| **Event** | HackPSU Fall 2026, Sat Oct 24 – Sun Oct 25, ECoRE Building, Penn State University Park |
| **Route** | Mystery Stack: *Phone motion* + *Rivalry* + *Group of 4+* |
| **Team** | Aditya Pratap Singh · Brian Podolskiy · Kenneth Tran · **Michael Shepherd (me)** · Ryan Smith |
| **Repo** | [Ryan-M-Smith/SkillIssue](https://github.com/Ryan-M-Smith/SkillIssue) (pnpm/npm monorepo) |
| **Website** | [skillissue.vodka](https://skillissue.vodka/) (Next.js on Vercel) |
| **Stack** | Godot 4.7.1 (GL Compatibility, Jolt) · Expo SDK 58 / React Native 0.88 · Node WebSocket relay · Next.js 16 · Tiger Data (Postgres) · Gemini (MVP judge) |
| **My role** | The **Duo** player character (components, controllers, hitboxes, weapons, model), the maps (Arena v2, **The Pit**), the **noir theme** for the game and phone app, and the website homepage swap |

> [!WARNING]
> **Evidence convention (carried over from the journal)**
> **Confirmed** means it's on `main`, in a commit, or was tested in these notes. **Proposed** means planned or designed but not verified in a running build. **Unknown** means not established. I don't invent hackathon results, awards, judge feedback or real-phone test results. Those sections stay blank until they happen.

## Map of the notes

### The idea
1. [01 Event & Challenge](notes/01-event-and-challenge.md): HackPSU, the Mystery Stack draw, the MLH × DEV writing challenge
2. [02 Pitch & Concept](notes/02-pitch-and-concept.md): elevator pitch, design pillars, the split-body idea
3. [03 Whiteboard Brainstorm](notes/03-whiteboard-brainstorm.md): the team's whiteboards (data boundaries, todos, controls, mechanics, wishlist)

### The build
4. [04 Team & Roles](notes/04-team-and-roles.md): who did what, confirmed from commits
5. [05 Architecture](notes/05-architecture.md): game ↔ relay ↔ phones ↔ website, data boundaries, the Duo's component design
6. [06 Match Flow & Rules](notes/06-match-flow-and-rules.md): lobby → match → results, rules, MVP
7. [07 Controls & Motion](notes/07-controls-and-motion.md): Runner/Gunner inputs and how they changed
8. [08 Duo Character](notes/08-duo-character.md): from crude boxes to the noir raccoon pair
9. [09 Weapons & Combat](notes/09-weapons-and-combat.md): hitboxes, spread, trails, pickups, scope, ammo, spawn protection, healing
10. [10 Maps](notes/10-maps.md): from Brian's first blockout to The Pit in the rain
11. [11 Game UI & Noir Theme](notes/11-game-ui-and-noir-theme.md): menus, lobby, HUD, scoreboard, results
12. [12 Phone App](notes/12-phone-app.md): the Expo companion and the iPhone/Expo Go situation
13. [13 Website](notes/13-website.md): skillissue.vodka, design system, homepage swap, standings removal
14. [14 Art Direction](notes/14-art-direction.md): what worked, what got thrown out, and the anatomy rule

### The process
15. [15 Git Workflow & PR History](notes/15-git-workflow-and-pr-history.md): rules, PRs #1–#11, branch cleanup
16. [16 Tuning](notes/16-tuning.md): numbers and the reasoning behind them
17. [17 Testing Log](notes/17-testing-log.md): everything tested and what broke
18. [18 Decision Log](notes/18-decision-log.md): every key decision with who made it and why
19. [19 Timeline](notes/19-timeline.md): hour by hour, Saturday 15:16 → Sunday 11:47
20. [20 MLH & Partner Tech](notes/20-mlh-and-partner-tech.md): Auth0, Tiger Data, Gemini, ElevenLabs, GoDaddy
21. [21 Open Items & Retrospective](notes/21-open-items-and-retrospective.md): what's left, lessons, postmortem prompts

### Writing
- [DEV Post Draft](writeup/dev-post-draft.md): MLH × DEV Writing Challenge (publish by Oct 31)
- [Portfolio Framing](writeup/portfolio-framing.md): résumé and portfolio wording, limited to what I actually built

## Status snapshot (Sun Oct 25, 11:47, `main` @ `6d291fc`)
- [x] Full game loop: menu → lobby code → phones join → team + role → match → results with MVP
- [x] Duo character, hitboxes, spread, trails, weapon pickups, scope, ammo, spawn protection, hat pop, death split
- [x] **The Pit** map with the **noir** theme (rain, neon, skyline)
- [x] Noir game UI (menu, lobby, results, case-file scoreboard) and noir phone app
- [x] Website live at skillissue.vodka with the approved hero; standings removed; Arsenal section added; lobby-code scramble
- [x] Phone movement reworked (Android sensors fixed, lateral tilt more responsive, gunner smoothing)
- [ ] Real 4-phone test at the venue (**unknown**: not recorded in these notes)
- [ ] Hackathon submission link, judging result, demo video (**unknown**)
- [ ] DEV post (due Oct 31)
