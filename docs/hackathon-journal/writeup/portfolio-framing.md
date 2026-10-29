---
tags: [portfolio, resume, skill-issue]
---
# Portfolio Framing

> [!WARNING]
> **Only claim what's mine**
> Every bullet below is backed by a commit or PR of mine ([04 Team & Roles](../notes/04-team-and-roles.md), [15 Git Workflow & PR History](../notes/15-git-workflow-and-pr-history.md)). Networking, the relay, the control plane, the Gemini MVP, motion sensing, the HUD and medkits were **teammates' work**. Credit them; don't list them as mine.

## Project description (team, neutral)
> **Skill Issue** is a 2v2 split-screen shooter built by a five-person team at HackPSU Fall 2026. Each team shares one character, two raccoons in a trench coat, controlled by two phones: one player moves with tilt gestures while the other aims with the gyroscope. Built with Godot 4.7, an Expo phone app, a Node WebSocket relay and a Next.js site on Vercel.

## My bullets (pick 3–4)
- Designed and built the **shared player character** in Godot 4.7: a component system (movement, aim, weapons, health, team, hitboxes) driven by a decoupled input layer, so two phones, a keyboard or a bot can control one body.
- Implemented **data-driven combat**: zone hitboxes, movement-dependent weapon spread with bloom, tracers, floating weapon pickups, gun models and a sniper scope with an enemy-visible glint.
- Built the game's **three-level arena ("The Pit")** with sightline-tested spawn rooms and spawn protection, then gave the whole game a **film-noir theme** (procedural surface shader, rain, neon, B&W UI kit) across the Godot game and the Expo phone app.
- Shipped **7 pull requests** (plus direct commits) into a shared monorepo with zero conflicts on teammates' files, using branch-per-feature, explicit staging and 3-way rebuilds when `main` moved.
- Swapped the production homepage behind a **one-line, reversible Next.js rewrite**, keeping all API routes untouched.

## One-liners
- *Short:* Built the player character, combat systems, map and noir art direction for a phone-controlled 2v2 shooter (HackPSU Fall 2026, team of 5).
- *For a game-dev role:* Godot 4 components, hitscan combat, level design, shaders.
- *For a web role:* Next.js rewrite-based homepage swap on Vercel; Expo UI theming.

## Links
- Repo: https://github.com/Ryan-M-Smith/SkillIssue
- Site: https://skillissue.vodka/
- Submission: *add*
- Demo video: *add*
