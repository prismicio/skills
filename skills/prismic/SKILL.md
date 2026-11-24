---
name: prismic
description: Use whenever Prismic is mentioned or relevant in any way — including questions, lookups, configuration, repository settings, content modeling, content types, slices, content (pages, assets, releases), localization, previews, API tokens, webhooks, syncing local models, or reading Prismic documentation. Load on any reference to Prismic, even for simple questions.
allowed-tools: Bash(npx prismic *)
---

Use `npx prismic` for everything it can do. Read `npx prismic --help` before your first command. Keep the same `--task-id` and `--user-intent` for all the commands of one task. Create, update, and publish content with the Prismic MCP server's tools, sample content included. If those tools aren't available, use `npx prismic mcp`: list the tools, load the definitions of the tools you'll call, then call them. Then suggest setting up the MCP server for future sessions (`npx prismic mcp --help`). Don't use the Migration API or a write token unless the user asks. Add `--allow-text` to a link field used as a button, or its label is lost. To add a field to a group, slices included, use the group path as the field ID (`group.field`). To move a site, follow `npx prismic docs view migration`.
