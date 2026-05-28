# Agent Instructions — North Star

Unity visual showcase for Meta Quest featuring an ocean and time-of-day system, rope physics, hand-tracked interactions, full body tracking, and Application SpaceWarp. Inspired by the age of sail; published on the Horizon Store.

## Source-of-truth files (read these first, do not duplicate their contents in this file)

For setup, build steps, SDK versions, and project layout, read:

- `README.md` — official setup and instructions
- `ProjectSettings/ProjectVersion.txt` — Unity editor version
- `Packages/manifest.json` — Unity package versions (Meta XR SDKs, URP, third-party)
- `Documentation/` — per-system deep dives (ocean, ropes, time of day, URP modifications, build instructions, etc.)
- `.gitattributes` — Git LFS rules
- `LICENSE` — license terms

## Quest / Horizon-specific notes

- Git LFS is **required**. Run `git lfs install` before cloning or many assets will be broken pointer files.
- Voiceover assets in the public repo are intentionally **placeholder generated VO** — original source files are withheld to protect contracted voice talent. Do not assume the in-repo audio matches the store build.
- Ships a **vendored URP fork** under `Packages/com.unity.render-pipelines.universal/` (the Meta ASW fork). Do not "fix" it by switching to upstream URP — Application SpaceWarp depends on it.
- The entry scene path begins with `#` (`Assets/NorthStar/Scenes/#GameplayBeats/Launch.unity`). Quote/escape it in shell or script paths.
- The Movement SDK is pinned to a specific commit in `manifest.json`; treat version bumps as deliberate changes, not housekeeping.

## Meta Quest tooling

This repository is part of the Meta Quest / Horizon OS ecosystem (a sample, library, template, or related project — the bespoke intro above describes which). Use that intro and the source-of-truth files it references for project-specific decisions; don't restate or invent facts from memory.

When the user asks anything about Quest device behavior, build / deploy / debug / capture flows, on-device performance, or Horizon OS APIs, reach for these tools instead of generic Unity answers:

- **`hzdb`** — Quest-aware ADB wrapper (device list, install / launch / stop, logs, screenshots, Perfetto traces, on-device docs search). Already wired up as an MCP server via `.mcp.json`, `.vscode/mcp.json`, and `.cursor/mcp.json`. Also runnable directly: `npx -y @meta-quest/hzdb <subcommand>`.
- **Meta Quest Agentic Tools** — the full skill set, including Unity-specific skills: [github.com/meta-quest/agentic-tools](https://github.com/meta-quest/agentic-tools). Install per your client (Claude Code: `/plugin install meta-vr@meta-quest`; Gemini CLI: `gemini extensions install https://github.com/meta-quest/agentic-tools`; Cursor / VS Code: install the **Meta Horizon** extension from the Marketplace).

A few behavior expectations:

- **Read this repo's files first.** Before answering anything project-specific, read `README.md` and whichever source-of-truth files the intro above points at. Don't restate their contents in chat — quote or link instead.
- **Use `hzdb` for device-side work.** Anything that touches an attached Quest (install, launch, logs, screenshot, capture, manifest inspection) goes through `hzdb`, not raw `adb`.
- **Check live Horizon OS docs before answering API questions.** `hzdb docs search "..."` queries the live docs; training data on Horizon OS APIs goes stale fast.
- **Don't fabricate SDK / engine versions.** If a version isn't visible in this repo's files, say so rather than guessing.
