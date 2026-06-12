# WAO Foundation stack — deployment

Portfolio documentation repo for the WAO Foundation digital stack. **Not a Coolify Next.js app.**

## One local + one live

| | Local / ops | Live production |
|--|-------------|-----------------|
| **Public site** | WordPress admin (managed host) | `https://waofoundation.org` |
| **Automation** | n8n editor on Hetzner VPS | Same VPS (self-hosted n8n) |
| **Static assets** | Cloudflare Pages project | Cloudflare CDN |

## Canonical source

- Repo: `https://github.com/truehubsolutions/wao-foundation-stack` (docs + architecture)
- Application code lives in WordPress theme, n8n workflows, and Cloudflare — not in this repo.

## THS ops index

Cross-app subdomain map: `truehubsolutions/family-hq` → `ops/ths-subdomains.md`

## Workflow

1. Change WordPress / n8n / Cloudflare in their respective consoles.
2. Update this repo README or ops notes when architecture changes.
3. No `npm run ship` — deploy is outside git push to Coolify.

**Sync:** copy this file to `DEPLOYMENT.md` on `truehubsolutions/wao-foundation-stack` when updating client docs.
