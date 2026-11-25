# Egretmarsh: Website

A one-page site for Egretmarsh, which provides Solo and self-directed 401(k) plan support from an
office in Tampa, Florida. It's static with no dependencies, built with Node and hosted on
**Cloudflare** (Workers static assets via `wrangler.jsonc`, or Pages).

## Quick start

```bash
node build.mjs          # builds ./dist; checks internal links; lists missing info
STRICT=1 node build.mjs # pre-launch check (fails while placeholders remain)
```

## Deploy to Cloudflare

**Workers (current setup):** Workers & Pages → Create → Import a repository → this repo.
Build command `npm run build`, deploy command `npx wrangler deploy`. `wrangler.jsonc` serves `./dist`.
Every push to the branch redeploys automatically.

**Pages (alternative):** Build command `node build.mjs`, output directory `dist`.

Security headers and redirects live in `src/static/_headers` and `src/static/_redirects`, which
are copied into `dist/` and applied by Cloudflare. After the first deploy, set `site.url` in
`site.config.mjs` to the live address (or custom domain) so canonicals, the sitemap and the form's
thank-you redirect are correct.

## Contact form (n8n)

The meeting form posts to an **n8n Webhook**, and the n8n workflow routes each submission
(email, sheet, CRM) and redirects the visitor to `/thank-you/`. Put the webhook's production URL
in `form.webhookUrl` in `site.config.mjs`. Until then the form shows a "not connected yet" notice
and won't send. Setup steps: `docs/N8N-FORM-SETUP.md`.

## Office

**3502 Henderson Blvd, Tampa, FL 33609** (storefront office). Phone: **(656) 223-5799**.

## Structure

The homepage (`/`) holds every section, each reachable from the menu and the sticky section bar:
Services · How it works · Who does what · 401(k) basics · FAQ · About · Visit & contact (meeting form).
`/privacy-policy/`, `/terms/` and `/disclosures/` are separate pages under Florida law,
plus `/thank-you/` and `404.html`.

## Design

- **Palette:** marsh night `#1C2B26`, sunset coral `#B04632` (buttons, white text), sunset amber `#E39A55`, peach `#F2B880`, marsh green `#4F7A5A`, linen `#F8F9F5`
- **Type:** Besley (display) and Sen (text), both self-hosted
- **Logo:** a tall oval badge with a great egret standing in marsh water among reeds at sunset (`src/brand.mjs`)
- **Hero:** slow-zoom photo of trees standing in calm water at sunset

See `docs/` for the launch checklist, media sources, Search Console and Google Business Profile steps.
