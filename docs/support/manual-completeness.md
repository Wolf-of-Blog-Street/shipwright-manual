# Manual completeness and publication

The public-facing Ship Manual is [`docs/viewers/ship-manual.html`](../viewers/ship-manual.html). It is the
single visual entry point for inspection and must contain the complete manual library, not merely a summary or
a set of links.

## Required contents

The Manual Library view must expose the complete source of all of these volumes:

- the owner's whole-ship manual: `docs/system/ship-manual.md`;
- the Captain inspection manuals: `docs/system/captain-harness-manual.md`, `docs/shipbook/shipbook-captain.md`,
  and `docs/shipbook/shipbook-commodore.md`;
- the operating handbook: `docs/system/how-to-run-the-ship.md`;
- the shared agent/officer standard: `docs/shipbook/shared/officer-operating-standard.md`;
- all ten department books under `docs/shipbook/departments/`; and
- the evidence-backed build view: `docs/viewers/ship-building.html` and its source register,
  `docs/system/ship-build-register.json`.

The HTML may present Markdown sources in an inspection frame, a generated rendering, or another accessible
in-page format. A link-only index is not complete. The page must label source authority and must preserve the
truth labels (`AS-BUILT`, `CONFIGURED`, `TARGET`, and `UNVERIFIED`) instead of implying that documentation is
runtime proof.

## Update rule

When any listed source changes, update or regenerate the visual Manual in the same change. Regenerate the
derived Captain volume and build view, then run:

```bash
node scripts/render-shipbooks.mjs --check
node scripts/render-ship-building.mjs
```

Review the Manual Library in a browser after rendering. Confirm that the owner's manual, Captain volumes, every
department book, and the build view are still present and readable. Do not hand-edit
`docs/shipbook/shipbook-captain.md`; it is generated from its source books.

## Publication rule

Only the visual HTML and the source files intentionally included in the publication package should be made
public. Do not publish the private repository, Brain records, credentials, research transcripts, or runtime
state merely to publish the Manual. The public URL must point to the visual Ship Manual, and a publication is
not ready to share until the complete-library check above passes.

The current scoped publication is:

- [public repository](https://github.com/Wolf-of-Blog-Street/shipwright-manual);
- [shareable visual manual](https://htmlpreview.github.io/?https://github.com/Wolf-of-Blog-Street/shipwright-manual/blob/main/docs/viewers/ship-manual.html).

GitHub Pages is not enabled for this organization, so the second link uses the public repository as its source
through the HTML Preview service. If a first-party static host is later authorized, replace the preview link
here and keep the scoped publication boundary unchanged.
