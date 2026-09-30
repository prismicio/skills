# Move a project from the Legacy Builder

Use this procedure when a repository uses the Legacy Builder, or when a type has legacy slices (slices defined inside the type's slice zone, not shared slices). The CLI and the Type Builder cannot edit legacy slices. You must convert them to shared slices.

## Rules

- The CLI supports Next.js, Nuxt, and SvelteKit projects only. If the project uses another framework, tell the user and stop.
- The git working tree must be clean before you start. Do the work on a new git branch.
- Convert one legacy slice at a time. Update its code before you convert the next one.
- Conversion changes local model files only. Stored documents do not change. After `npx prismic push`, the Content API returns legacy content in the shared slice shape as soon as the master ref changes. Any publish changes the master ref, also for documents that nobody edits. Thus you must deploy the updated code at the same time as the push.
- After a conversion, write content for that slice as a shared slice. The Migration API rejects the legacy format.

## Procedure

1. Set up the project:
   - If `slicemachine.config.json` exists, run `npx prismic init`. Otherwise, run `npx prismic init --repo <domain>`.
   - On a Legacy Builder repository, `init` turns on the Type Builder. Only a repository administrator can do this. If `init` reports that an administrator is necessary, tell the user and stop.
   - `init` prints the number of legacy slices to convert.
2. If the repository has environments (`npx prismic env list`), tell the user to test on an environment first. Run `npx prismic env set <environment-domain>` before you push. Read `npx prismic env --help`.
3. Run `npx prismic slice migrate` to list the legacy slices. Each row shows the slice ID, type, slice zone, kind (`Slice`, `Group`, or a field type), and a suggested command. Use `--json` for machine-readable output. Read `npx prismic slice migrate --help` for all options.
4. Convert one slice with its suggested command:
   - `npx prismic slice migrate <id> --from <type-id>` creates a shared slice with the same ID and a `default` variation.
   - The suggested command for a second legacy slice with the same ID uses `--to <id>`. It merges the slice into a variation with identical fields, or adds a new variation.
   - Use `--to <other-slice>`, `--variation <id>`, or `--id <new-id>` only when the fields are identical or the user asks for it. These options change `slice_type`.
   - If two legacy slices have the same ID but different fields, ask the user whether to add a variation (`--to <id> --variation <new-variation>`) or create a separate slice (`--id <new-id>`).
5. Update the code for that slice. The command prints the content changes and the path of the slice component. Apply the changes from the table below.
6. Run the project's type check and start the site. Make sure that pages with the slice render.
7. Commit the changes. Before you push to the production repository, ask the user for confirmation: the live site shows broken slices until the updated code is deployed. Then run `npx prismic push` and tell the user to deploy the code at the same time.
8. Go to step 3. Stop when `npx prismic slice migrate` prints "No legacy slices found."

## Content changes

`slice_label` does not change in any case.

| Conversion | Content shape after the push | Code changes |
| --- | --- | --- |
| Legacy `Slice` to a new shared slice | `slice_type`, `id`, `primary`, and `items` do not change. `variation: "default"` and `version` are added. | Move the old component's code into the component that the CLI created. Register it in the slice library index or components map under the same `slice_type`. Remove the old component and its registration. Update types to the generated shared slice type. |
| Legacy `Group` | `slice.value` (array) moves to `slice.items`. `slice.primary` is `{}`. | Same as above. Also replace `slice.value` with `slice.items`. |
| Legacy field (for example a Text field) | `slice.value` moves to `slice.primary.<legacy-id>`. `slice.items` is `[]`. | Same as above. Also replace `slice.value` with `slice.primary.<legacy-id>`. |
| Merge into an identical variation (`--to <slice>`) | `slice_type` becomes `<slice>`. The `id` prefix changes. The variation is the merged variation. | The `<slice>` component renders this content. Remove the old component and its registration. Update code that uses the old `slice_type`. |
| New variation (`--to <slice> --variation <variation>`) | `slice_type` becomes `<slice>`. `variation` becomes `<variation>`. | Move the old component's code into the `<slice>` component and branch on `slice.variation`. Remove the old component and its registration. Update code that uses the old `slice_type`. |
| New ID (`--id <new-id>`) | `slice_type` becomes `<new-id>`. | Move the old component's code into the new component. Update code that uses the old `slice_type`. |
