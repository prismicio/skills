---
name: prismic
description: Use whenever Prismic is mentioned or relevant in any way — including questions, lookups, configuration, repository settings, content modeling, content types, slices, content (pages, assets, releases), localization, previews, API tokens, webhooks, syncing local models, or reading Prismic documentation. Load on any reference to Prismic, even for simple questions.
allowed-tools: Bash(npx prismic *)
---

Prismic is a headless CMS. Use the `prismic` CLI for models and settings, and the Prismic MCP server for content.

1. Run commands with `npx prismic`. Learn them from `npx prismic --help` and `npx prismic <command> --help`. Don't guess the syntax.
2. Change models only with the CLI, never by editing their JSON files.
3. Write content with the MCP server, sample content included, not the Migration API. If it isn't connected, ask the user to connect it (`npx prismic docs view mcp`). To move a site, follow `npx prismic docs view migration`.
4. Run `npx prismic` commands without asking, including ones that create a repository. Ask before removing anything, and use `--force` only when asked.
