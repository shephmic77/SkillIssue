---
tags: [mlh, sponsors, partner-tech, skill-issue]
---
# MLH & Partner Tech

The whiteboards had sponsor tech in mind from the start: **"Auth0 → Tiger"** and **"ElevenLabs: pre-generated voice lines/reactions?"** ([03 Whiteboard Brainstorm](03-whiteboard-brainstorm.md)), plus **"MLH: Tiger Data"** next to the controls sketch.

| Tech | What it's for in Skill Issue | Status (Sun 11:47) |
|---|---|---|
| **Tiger Data** (Tiger Cloud, Postgres-compatible) | Durable data: accounts, matches, **leaderboard** (`leaderboard_entries` table, top 10 by score). Never live input. | API route on `main` (`/api/leaderboard`, returns 503 / `source: "unconfigured"` without `TIGER_DATABASE_URL`). **Not shown on the website** any more. Accounts + match upload are on the open `claude/mlh-tracks` branch. |
| **Auth0** | Sign-in for the phone app, game and website | **Open branch** `claude/mlh-tracks` (Ryan, Sun 05:16). Setup was paused for Ryan earlier. Not on `main`. |
| **Google Gemini** | Judges the **match MVP** (`/api/mvp`) and draws a **raccoon badge** (`/api/mvp/badge`); no-MVP noir scene | **On `main`** (Ryan). Needs `GEMINI_API_KEY` in Vercel; falls back to a local rule. |
| **ElevenLabs** | Pre-generated voice lines / reactions | **Idea only.** The game has no sound on `main` yet; music and SFX are on `powerups`. |
| **GoDaddy** | Domain | Was part of the paused MLH setup. *Which registrar `skillissue.vodka` uses is unknown here.* |
| **Vercel** | Hosting + preview deployments for `apps/landing` | Live |
| **Render** | Hosting option for the Node relay (`apps/server`) | Documented in the README |

## Tiger Data table (from `docs/tiger-data.md`)
```sql
CREATE TABLE leaderboard_entries (
    player_id    text PRIMARY KEY,
    display_name text NOT NULL,
    wins         integer NOT NULL DEFAULT 0,
    losses       integer NOT NULL DEFAULT 0,
    score        integer NOT NULL DEFAULT 0,
    updated_at   timestamptz NOT NULL DEFAULT now()
);
```
```ts
type LeaderboardResponse = {
  entries: { playerId: string; displayName: string; wins: number;
             losses: number; score: number; updatedAt: string }[];
  source: string;      // e.g. "unconfigured"
  message?: string;
};
```
The browser only ever gets ranked rows. The database URL stays server-side. Match results should be written by the relay or a trusted server action, never the browser.

## To claim a partner-tech prize or mention it in the DEV post
- [ ] Decide whether `claude/mlh-tracks` merges (Auth0 + Tiger accounts/matches)
- [ ] Set `TIGER_DATABASE_URL` and create the table, or say honestly that Tiger is wired but not deployed
- [ ] Gemini MVP is live: describe it under **Partner Technologies**
- [ ] Don't list ElevenLabs or Auth0 as "used" unless they ship
