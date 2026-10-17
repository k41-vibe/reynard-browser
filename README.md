<img width="100" height="100" src="https://github.com/user-attachments/assets/1c42dda2-b778-4342-9f94-8f852c3ad652" />

# Reynard (LiveContainer build)

This is a personal fork of [Reynard Browser](https://github.com/minh-ton/reynard-browser), a Gecko-based web browser for iOS. It changes one thing: when Reynard runs inside LiveContainer, its child processes (`Reynard Helper.appex`) start through LiveContainer's `LiveProcess.appex`.

> [!WARNING]
> This is an experimental test build and has not been confirmed on a real device yet.
> It is not affiliated with the Reynard project. Please do not report issues from this build to upstream.

## Downloads

The build is attached to the [v0.17.0-lc1 release](https://github.com/k41-vibe/reynard-lc/releases/tag/v0.17.0-lc1) of `reynard-lc`.

## Requirements

Reynard needs a LiveContainer that can host guest App Extensions. The official LiveContainer cannot do this. Use one of the builds from [k41-vibe/LiveContainer](https://github.com/k41-vibe/LiveContainer/releases/tag/v3.8.10-rc1).

| LiveContainer build | Notes |
|---|---|
| `LiveContainer-RC-lite.ipa` | Installs next to regular LiveContainer |
| `LiveContainer-extswap.ipa` | Replaces regular LiveContainer |

Outside LiveContainer, this build behaves like upstream Reynard.

## Installation

1. Install one of the LiveContainer builds above with **Keep App Extensions** selected.
2. In LiveContainer, import `Reynard.ipa` and choose Keep App Extensions again.
3. Open Reynard and load a website.

If it fails, collect logs from a computer with `idevicesyslog | grep -E "GuestExtension|NSExtension"`.

## Differences from upstream

- `patches/ipc/glue/NSExtensionUtils.mm.patch`: when the host app has a `LiveProcess.appex`, Reynard sends the child extension request to it. The request includes `lcGuestExtensionPath`, `lcGuestExtensionPrincipalClass` and `lcGuestExtensionInputItems`. Without LiveContainer, it uses the system extension registry as before.

Full diff: [main...livecontainer-ext-host](https://github.com/k41-vibe/reynard-browser/compare/main...livecontainer-ext-host)

## Repositories and branches

| Repository | Role |
|---|---|
| [k41-vibe/reynard-browser](https://github.com/k41-vibe/reynard-browser) | GitHub fork of upstream, used for the source |
| [k41-vibe/reynard-lc](https://github.com/k41-vibe/reynard-lc) | Copy of the same branches, used for Actions builds and releases |

| Branch | Contents |
|---|---|
| `main` | Upstream Reynard and this README |
| `livecontainer-ext-host` | The LiveContainer build, based on upstream 0.17.0 |

For build instructions, see the [upstream README](https://github.com/minh-ton/reynard-browser#readme).

## Credits and license

Reynard Browser is developed by [minh-ton](https://github.com/minh-ton) and contributors. This fork is distributed under the same [GNU GPL-3.0](./LICENSE) license as upstream.
