# Codex Readable Source: Launch Guide

This folder contains a readable, unpacked Electron app.

## Paths Used In This Workspace

- App source: `/Users/igor/temp/untitled folder 67/codex_reverse/readable`
- Electron binary: `/Users/igor/temp/untitled folder 67/codex_reverse/meta/electron-runner/node_modules/.bin/electron`
- Codex CLI binary: `/opt/homebrew/bin/codex`

## Prerequisites

1. Electron runner binary exists at the path above.
2. Codex CLI exists (`/opt/homebrew/bin/codex`).

## Launch Desktop Mode (non-web)

Use this command:

```bash
env \
  ELECTRON_RENDERER_URL='file:///Users/igor/temp/untitled%20folder%2067/codex_reverse/readable/webview/index.html' \
  CODEX_CLI_PATH='/opt/homebrew/bin/codex' \
  CUSTOM_CLI_PATH='/opt/homebrew/bin/codex' \
  '/Users/igor/temp/untitled folder 67/codex_reverse/meta/electron-runner/node_modules/.bin/electron' \
  '/Users/igor/temp/untitled folder 67/codex_reverse/readable'
```

Notes:
- `ELECTRON_RENDERER_URL` is required in this unpacked source setup so desktop mode loads local renderer assets instead of `http://localhost:5175/`.
- `CODEX_CLI_PATH`/`CUSTOM_CLI_PATH` prevent `Unable to locate the Codex CLI binary`.

## Launch Web Mode

Local-only (recommended):

```bash
env \
  CODEX_CLI_PATH='/opt/homebrew/bin/codex' \
  CUSTOM_CLI_PATH='/opt/homebrew/bin/codex' \
  '/Users/igor/temp/untitled folder 67/codex_reverse/meta/electron-runner/node_modules/.bin/electron' \
  '/Users/igor/temp/untitled folder 67/codex_reverse/readable' \
  --webui --port 4310
```

Open in browser:

- `http://127.0.0.1:4310/`

Remote/LAN binding:

```bash
env \
  CODEX_CLI_PATH='/opt/homebrew/bin/codex' \
  CUSTOM_CLI_PATH='/opt/homebrew/bin/codex' \
  '/Users/igor/temp/untitled folder 67/codex_reverse/meta/electron-runner/node_modules/.bin/electron' \
  '/Users/igor/temp/untitled folder 67/codex_reverse/readable' \
  --webui --remote --port 4310 --token YOUR_TOKEN
```

## Verify Web Mode

```bash
curl -I 'http://127.0.0.1:4310/'
```

Expected: `HTTP/1.1 200 OK`

## Stop The Running App

If running in foreground: press `Ctrl+C`.

If running in background:

```bash
lsof -nP -iTCP:4310 -sTCP:LISTEN
kill <PID>
```
