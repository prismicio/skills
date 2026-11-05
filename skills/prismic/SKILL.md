---
name: prismic
description: Use whenever Prismic is mentioned or relevant in any way — including questions, lookups, configuration, repository settings, content modeling, content types, slices, content (pages, assets, releases), localization, previews, API tokens, webhooks, syncing local models, or reading Prismic documentation. Load on any reference to Prismic, even for simple questions.
allowed-tools: Bash(npx prismic *)
---

Prismic is a headless CMS. The `prismic` CLI manages content models, repository settings, and documentation. The Prismic MCP server manages content.

1. Run commands with `npx prismic`. Learn them from `npx prismic --help` and `npx prismic <command> --help`. Don't guess the syntax.
2. Change models only with the CLI, never by editing their JSON files.
3. Create, update, and publish content with the Prismic MCP server, sample content included. Don't use the Migration API or a write token unless the user asks. To move an existing site, follow the migration guide (`npx prismic docs view migration`). If the MCP server isn't connected, ask the user to connect it (`npx prismic docs view mcp`).
4. Run `npx prismic` commands without asking, including ones that create a repository. Ask before removing anything, and use `--force` only when asked.
