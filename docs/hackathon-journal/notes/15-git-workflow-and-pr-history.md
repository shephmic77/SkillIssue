---
tags: [git, github, workflow, pull-requests, skill-issue]
---
# Git Workflow & PR History

## Setup
- **Repo:** `Ryan-M-Smith/SkillIssue`, default branch `main`.
- **My clone:** `C:\Users\mikey\Documents\SkillIssue`. PowerShell opens in my home folder, so every session starts with `cd "C:\Users\mikey\Documents\SkillIssue"`.
- **Downloads** (zips and files from Claude) land in `C:\Users\mikey\Desktop\2v2` or `Downloads`.
- `git config pull.rebase true` (team rule), so pulls replay my commits on top instead of making merge commits.
- `git config --global credential.helper manager`: the first push failed with "Invalid username or token" until this was set.
- Commit email: GitHub **no-reply** (`131554214+shephmic77@users.noreply.github.com`), since "Keep my email private" is on.

## My loop for every feature
```powershell
cd "C:\Users\mikey\Documents\SkillIssue"
git checkout main; git pull                      # stash -u first if anything is uncommitted
git checkout -b <feature>
Expand-Archive "$HOME\Desktop\2v2\<zip>.zip" -DestinationPath . -Force
git status                                       # only the expected files?
git diff -- "*.tscn"                             # read scene diffs line by line
git add <explicit paths>                         # never "git add ."
git diff --cached --stat
git commit -m "<what it does>"
git push -u origin <feature>
# GitHub: Compare & pull request → check the Vercel preview if the site changed → Merge
git checkout main; git pull
git branch -d <feature>; git push origin --delete <feature>
git fetch --prune
```

## Rules learned the hard way
1. **Check what changed in scene files, not just which files.** A `.tscn` showed 12 changed lines instead of 9; Godot had saved an accidental **157° map rotation** into it. Always read `git diff --cached -- "*.tscn"`.
2. **When `main` moves, rebuild on it; never drop in an old copy.** My hitboxes zip predated teammates' sprint edits, so I rebuilt it with a **3-way merge** (16 of 17 files merged automatically; one comment conflict resolved by keeping both).
3. **Fetch before pull.** `git fetch` then `git log --oneline main..origin/main` shows teammates' work without changing anything. That's how I caught a teammate's `GameEvents` with the same name as mine.
4. **Uncommitted work follows you between branches.** Noir changes carried over onto `main` when I switched. Fix: `git stash -u`, delete the stale branch, unzip again on a fresh branch.
5. **"We couldn't merge this pull request"** (PR #10): `main` had moved. Updating the branch and retrying merged cleanly.
6. **Ryan force-pushed `main` twice** (Sat ~23:45) to fix committer names. I compared before and after (zero file changes) and re-synced with `git fetch` + `git reset --hard origin/main`, which was safe only because I had no local work on `main`.
7. **Delete branches once they're in `main`.** After every merge I deleted the branch locally and on GitHub, then ran `git fetch --prune`.
8. **Paste only commands into PowerShell**, never a chat transcript.

## Pull requests
| # | Branch | By | What | Merged |
|---|---|---|---|---|
| 1 | `duo-components` | **me** | Duo player: components, controllers, crude model, split-screen test scene. 46 new files, **0 existing files changed**. Commit `4bad69c` | Sat 19:01 (`a80525e`) |
| 2 | `claude/charming-clarke-ajexy9` | Ryan | Fix phone movement to match the gesture spec | Sat 23:10 |
| 3 | same | Ryan | Rewrite gesture detection around the phone's X/Y/Z axes | Sat 23:32 |
| 4 | same | Ryan | Stream the phone to a web debugger with a live 3D view | Sun 00:26 |
| 5 | same | Ryan | Landscape phone controller that drives the game | Sun 00:42 |
| 6 | `hitboxes-spread` | **me** | Tunable hitboxes, spread, gun trails, F3 debug view (17 files, `d832e00`) | Sun 00:58 (`12cefee`) |
| 7 | `player-model-v2` | **me** | Simpler keyboard, empty pickup guns vanish, slim low-poly raccoon (`d38ef52`) | Sun 03:29 (`f25a4d0`) |
| 8 | `noir-theme` | **me** | Noir: rainy city map, B&W menus, lobby, end screen, case-file scoreboard (`b2a71f5`, 14 files) | Sun 09:16 (`5083a1b`) |
| 9 | `app-noir` | **me** | Phone app noir: brick-wall backdrop, B&W menus, lobby, team select, game over (`101dc5a`) | Sun 10:00 (`01974ba`) |
| 10 | `home-preview` | **me** | Serve `home-preview.html` at `/` (`59dd89e`) | Sun 11:05 (`74994a7`) |
| 11 | `remove-standings` | **me** | Remove the standings section and its links (`6435ae2`) | Sun 11:18 (`ea29adb`) |

**Not through a PR:**
- Weapon pickups / gun models / scope landed as "minor changes" (`5541944`, Sun 03:06), before PR #7.
- The Pit, spawn rooms + protection, hat FX and raccoon polish landed as a direct commit (`9fae05f`, Sun 05:05).
- Most of Ryan's Sunday work merged from `claude/*` branches without numbered PRs.

## Branches at Sun 11:47
| Branch | Owner | State |
|---|---|---|
| `main` | — | `6d291fc` |
| `andmotion` | Aditya | Fully merged into `main`; can be deleted when Aditya agrees |
| `powerups` | Kenneth | **Open**: bounty, mystery power-ups, swap on death, music crossfade, SFX autoload |
| `claude/mlh-tracks` | Ryan | **Open**: Auth0 sign-in (phone, game, website), Tiger Data accounts/matches/leaderboards, match upload |
| `claude/reworked-movement` | Ryan | Merged (`d359a02`); can be deleted |
| Tag `site-before-preview` | me | The old homepage; delete once the new one is final |
