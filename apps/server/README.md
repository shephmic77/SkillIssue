# Relay server (`apps/server`)

A standalone Node.js WebSocket relay. It passes lobby, motion and match messages between the Godot game and the four phones.

You usually **don't need it for local play**: the Godot game runs the same lobby server itself on port 8080 when you choose **Create a Lobby**. Use this relay to host lobbies on the internet, or to test the network code without Godot.

## Run it

From the repository root:

```sh
npm run server:start      # listens on PORT (default 8080)
npm run test:network      # integration tests
```

With `GODOT_BIN` set, the network tests also run against the server built into Godot.

## Settings

| Variable | Default | Does |
| --- | --- | --- |
| `PORT` | `8080` | Port to listen on |
| `PUBLIC_WS_URL` | (none) | The public `wss://` address to hand out, when the relay runs behind a TLS proxy |
| `MIN_CONTROLLERS` | `4` | Phones needed before a match can start; set `1` to test with one phone |

## Deploying

On Render: build command `npm install`, start command `npm run server:start`. Put it behind TLS and point the website's `NEXT_PUBLIC_GAME_SERVER` at its `wss://` URL. Details are in [online play setup](../../docs/online-play-setup.md).

The message format is defined in [`packages/protocol`](../../packages/protocol/README.md) and described in [docs/network-protocol.md](../../docs/network-protocol.md).
