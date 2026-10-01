---
name: migrate-to-prismic
description: Use when moving an existing website or CMS (WordPress, Contentful, Sanity, Storyblok, Webflow, Drupal, a static site, etc.) to Prismic, in full or in part (e.g. "move our blog to Prismic"). Covers exporting the content, modeling it in Prismic, and importing pages, assets, and links.
allowed-tools: Bash(npx prismic *)
---

Stop for the user's review after each step below, unless they said not to. Use the Prismic CLI for the repository, locales, and models, and the Prismic MCP for content and assets. If the MCP tools are missing, ask the user to connect `https://mcp.prismic.io/mcp`, and export and model in the meantime.

## 1. Export

Define the scope with the user: the site URL, the source CMS and how to access it, which pages to migrate, and the locales. Users often migrate only part of a site.

- Export the content with a script that calls the CMS's API (its official SDK first). Write one JSON file per document in `migration/export/<type>/`, and check counts against the source. Without an API, use an export file from the user. Scrape the site only as a last resort.
- Group the sitemap's URLs by pattern and map each pattern to a type. Routes and internal links need this map.
- Note what the site shows but the CMS doesn't hold: navigation, footer, SEO metadata.
- Tell the user what you found: types with counts, URL patterns, fields, repeated sections, and what won't be migrated.

## 2. Model

The models decide the quality of the migration. Iterate until the user approves them.

- Read `npx prismic docs view content-modeling` first, and follow the CLI's help texts.
- Add routes to `prismic.config.json` that match the old URLs.
- Check that every exported field has a place, and list what you dropped. Then run `npx prismic push` and ask the user to review the models in the Type Builder.

## 3. Import

- A release holds at most 1,000 documents. Create one release per 1,000 documents, and tell the user the count before you start.
- Build documents from `get_custom_type`'s `emptyContent`, and copy field formats from `get_field_shapes`.
- Write settings and navigation first, then referenced types (authors, categories), then pages. Create each master-locale document before its translations. A translation can join its master only at creation.
- Look documents up by UID before creating them, and search assets before uploading them, so that a rerun doesn't duplicate anything.
- Upload each source asset once and use it everywhere, including images in rich text. Links to files such as PDFs become media links.
- Internal links become document links, including in navigation, CTAs, and rich text. Create the documents first, then add their links in a second pass with `update_document`.
- In rich text, use only the block types the field allows. Move tables, videos, and embeds into slices. Log content you can't map instead of dropping it.
- For each type, create one or two documents and have the user check them before you do the rest. Group failures by cause, and retry only the failed documents.
