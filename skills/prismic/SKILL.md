---
name: prismic
description: Use whenever Prismic is mentioned or relevant in any way — including questions, lookups, configuration, repository settings, content modeling, content types, slices, localization, previews, API tokens, webhooks, syncing local models, or reading Prismic documentation. Load on any reference to Prismic, even for simple questions.
allowed-tools: Bash(npx prismic *)
---

Prismic is a headless CMS. The `prismic` CLI manages content models, repository settings, and documentation.

1. Always run commands via `npx prismic`. Do not guess command syntax.
2. Start with `npx prismic --help` to learn available commands. Inspect details with `npx prismic <command> --help`.
3. Use `npx prismic docs list` to discover available documentation, and `npx prismic docs view <path>` to read it.
4. Prefer CLI workflows over direct API/manual changes. Never directly edit model JSON files (custom types, slices, etc.) — always use the CLI to make model changes.
5. If the CLI does not support a required operation, state that explicitly to the user and ask how they'd like to proceed.
6. Page URLs (routes) live in `prismic.config.json`. This file is project configuration, not a model file, so edit it directly. There is no route command. Run `npx prismic docs view routes` for the route format.
