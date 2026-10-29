# Shared protocol (`packages/protocol`)

`events.ts` defines every message the game, the phones and the relay send each other, as TypeScript types: lobby join and ready, team and role assignment, motion and button input, match status, and game over.

| Used by | Files |
| --- | --- |
| Phone app | `apps/companion/src/service/lobby-client.ts`, `debug-link.ts`, `screens/phone/game-over.tsx` |
| Relay | `apps/server/index.ts` |
| Godot game (mirrors the same messages in GDScript) | `apps/game/scripts/network/lobby_server.gd`, `network_client.gd`, `motion_interpreter.gd` |

The game can't import TypeScript, so when a message changes, update `events.ts` **and** the matching GDScript, then bump `protocolVersion`.

The full contract, with examples, is in [docs/network-protocol.md](../../docs/network-protocol.md).
