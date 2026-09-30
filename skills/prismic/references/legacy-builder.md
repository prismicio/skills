# Move a project from the Legacy Builder

Use this procedure when a repository uses the Legacy Builder or a type has legacy slices. The CLI and the Type Builder cannot edit legacy slices, so you must convert them to shared slices.

## Rules

- The CLI supports only Next.js, Nuxt, and SvelteKit. For another framework, tell the user and stop.
- Start from a clean git working tree on a new branch.
- Convert one legacy slice at a time, and update its code before the next one.
- After `npx prismic push`, the Content API returns converted content in the new shape as soon as anyone publishes, for every document. Deploy the updated code together with the push.
- Write new content for a converted slice in the shared slice format. The Migration API rejects the legacy format.

## Procedure

1. Run `npx prismic init` (add `--repo <domain>` if there is no `slicemachine.config.json`). On a Legacy Builder repository, it turns on the Type Builder. If it reports that an administrator is necessary, tell the user and stop.
2. If `npx prismic env list` shows environments, tell the user to test on one first with `npx prismic env set <environment-domain>`.
3. Run `npx prismic slice migrate` to list legacy slices with a suggested command for each.
4. Run the suggested command. If two legacy slices have the same ID but different fields, ask the user whether to add a variation with `--to <id> --variation <new-variation>`. See `npx prismic slice migrate --help`.
5. Update the code with the content changes that the command prints and the table below. Move the old component's code into the slice component, register it in the slice library or components map, and remove the old component.
6. Run the type check and start the site. Make sure that pages with the slice render.
7. Commit. Ask the user before you push to production, because the live site breaks until the new code is deployed. Run `npx prismic push` and tell the user to deploy at the same time.
8. Repeat from step 3 until the command prints "No legacy slices found."

## Content changes

| Conversion | Content after the push |
| --- | --- |
| Legacy `Slice` | `slice_type`, `primary`, and `items` do not change. `variation: "default"` is added. |
| Legacy `Group` | `slice.value` moves to `slice.items`. |
| Legacy field | `slice.value` moves to `slice.primary.<legacy-id>`. |
| `--to <slice>` | `slice_type` becomes `<slice>` and `slice.variation` the variation ID. The `<slice>` component renders it. Branch on `slice.variation` if it has several variations. |

`slice_label` does not change.
