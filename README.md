# forgegen-web

Static landing site for forgegen. Deployed to **forgegen.app** via Cloudflare
(Workers Assets).

## Structure

- `index.html` — single-page site: hero, features, how-it-works, requirements,
  cross-links to the rest of the Liquid Releasing family, download CTA.
- `latest-version.json` — version-badge data. Updated automatically by the
  `.github/workflows/sync-version.yml` workflow when a new release lands on
  `liquid-releasing/forgegen-releases`.
- Image assets — product branding (`forgegen_*`), forge-metaphor icons shared
  with the FunscriptForge / ForgeAssembler sites (`anvil.png`, `worktable.png`,
  etc.), Liquid Releasing badge (`Icon-Only-White.svg`).

## Local preview

```bash
# any static server works — python stdlib is fine:
python -m http.server 8080
# open http://localhost:8080
```

## Deployment

Cloudflare Workers Assets watches the `main` branch of this repo. Every push
auto-builds and deploys to `forgegen.app`. No build step — the site is static
HTML + assets.

## Release version badge

The hero's "version" line reads from `latest-version.json` via a small inline
fetch. When the forgegen release workflow publishes a new tag, it can fire a
`repository_dispatch` event against this repo; `sync-version.yml` catches it,
writes the new tag into `latest-version.json`, and commits to `main`. Manual
`workflow_dispatch` is also supported for backfills.

## Cross-links

This site cross-links to:

- [funscriptforge.com](https://funscriptforge.com) — FunscriptForge (downstream
  editing tool that consumes forgegen's `analysis.json` sidecar)
- [forgeassembler.app](https://forgeassembler.app) — ForgeAssembler (combines
  multiple finished clips into one long output)
- ForgeYT release artifacts on GitHub (no separate site yet)

Conversely, `funscriptforge.com` and `forgeassembler.app` link back here.

## License

Site content (c) 2026 Liquid Releasing. forgegen itself is MIT-licensed —
see the [main repo](https://github.com/liquid-releasing/forgegen).
