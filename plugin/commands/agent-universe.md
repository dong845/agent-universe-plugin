---
allowed-tools: Bash(curl -s http://127.0.0.1:5182/api/status:*), Bash(nohup npx -y agent-universe@latest:*), Bash(open http://127.0.0.1:5182/:*), Bash(xdg-open http://127.0.0.1:5182/:*), Bash(sleep:*)
description: Open Agent Universe (your Claude Code and Codex work as a universe, local only)
---

Open Agent Universe for the user. It is a local page at http://127.0.0.1:5182/ served by the npm
package `agent-universe`; it reads Claude Code and Codex logs on this computer and sends nothing anywhere.

1. Check whether it is already running: `curl -s http://127.0.0.1:5182/api/status`. If that prints JSON
   with a `phase` field, it is running: go to step 3.
2. Otherwise start it in the background, so this session is not blocked:
   `nohup npx -y agent-universe@latest --no-open > /tmp/agent-universe.log 2>&1 &`
   The first run downloads the package (a few MB). Then check the status again every few seconds
   (`sleep 3` between tries, at most ~60 seconds). If it never answers, show the last lines of
   /tmp/agent-universe.log and stop. Node 22.18 or newer is required; if the log says Node is too old,
   tell the user to install the current LTS from https://nodejs.org.
3. Open the page: `open http://127.0.0.1:5182/` on macOS, `xdg-open http://127.0.0.1:5182/` on Linux.
   Then reply in one or two sentences, in the user's language, with the link
   http://127.0.0.1:5182/ and a note that while it reads the logs the first time the page shows progress.

Do not do anything else.
