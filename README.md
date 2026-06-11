# nextepisode

A small holding page for **nextepisode.nz** — "this is where Adrian is trying
things." Black page, the site logo, and links to the two current projects.

No build step, no dependencies: a single self-contained `index.html` (CSS inlined),
plus the favicon and self-hosted Roboto fonts.

## Projects it links to

| Project | Linked at | Hosted on | Repo |
| --- | --- | --- | --- |
| **Te Papa Collections Browser** | `browser.nextepisode.nz` | Vercel | [tepapa-api-browser](https://github.com/adriankingston/tepapa-api-browser) |
| **Te Papa Digital Museum** | `museum.nextepisode.nz` | Railway | [tepapa-digital-museum](https://github.com/adriankingston/tepapa-digital-museum) |

Each app stays exactly where it already runs; the domain just points at it via a
subdomain — no changes to either app.

```
nextepisode.nz          →  this holding page   (Vercel — this repo)
browser.nextepisode.nz  →  Collections Browser (Vercel — existing project)
museum.nextepisode.nz   →  Digital Museum      (Railway — existing project)
```

> The two project links use the subdomains above, so they go live once the DNS
> records below are in place.

## Deploy

### 1. The holding page (apex)

```sh
npm i -g vercel        # if you don't have it
vercel                 # first run: link / create the project
vercel --prod          # deploy to production
```

Or push this repo to GitHub and import it in the Vercel dashboard (Framework
preset: **Other**; no build command; output dir is the repo root).

Then add the apex domain to this Vercel project: **Settings → Domains → add
`nextepisode.nz`** (and let it redirect `www`). Follow the DNS records Vercel shows.

### 2. `browser.` → the existing Vercel browser project

In the **tepapa-api-browser** Vercel project: **Settings → Domains → add
`browser.nextepisode.nz`**, then add the `CNAME` Vercel gives you (usually
`cname.vercel-dns.com`) at your DNS provider.

### 3. `museum.` → the existing Railway museum project

In Railway: **museum service → Settings → Networking → Custom Domain → add
`museum.nextepisode.nz`**, then add the `CNAME` target Railway returns.

### DNS summary

| Record | Name | Points to |
| --- | --- | --- |
| `A` / nameservers | `@` (apex) | Vercel (per its dashboard) |
| `CNAME` | `browser` | `cname.vercel-dns.com` (per Vercel) |
| `CNAME` | `museum` | the target Railway shows you |

## Local preview

It's static — open `index.html`, or serve the folder:

```sh
python3 -m http.server 4200      # → http://localhost:4200
```

## Notes

- The on-page logo is an inline SVG of the favicon's network mark, drawn white and
  animated (a three-state stepped cycle — rotation + node extend/contract + a white
  → teal → orange colour shift). The `favicon.svg` file itself is untouched and
  still serves as the browser-tab icon.
- Carries `noindex` (meta + `X-Robots-Tag` + `robots.txt`). Remove those if you
  want the page in search results.
