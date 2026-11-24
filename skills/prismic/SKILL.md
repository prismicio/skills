---
name: prismic
description: Use whenever Prismic is mentioned or relevant in any way — including questions, lookups, configuration, repository settings, content modeling, content types, slices, content (pages, assets, releases), localization, previews, API tokens, webhooks, syncing local models, or reading Prismic documentation. Load on any reference to Prismic, even for simple questions.
allowed-tools: Bash(npx prismic *)
---

Use `npx prismic` for everything it can do. Read `npx prismic --help` before your first command. Create, update, and publish content with the Prismic MCP server, sample content included. Don't use the Migration API or a write token unless the user asks. If the MCP server isn't connected, use `npx prismic mcp` to list its tools, load their definitions, and call them. Then suggest setting it up for future sessions (`npx prismic mcp --help`). To move a site, follow `npx prismic docs view migration`.
