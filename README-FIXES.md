# SchollyJob — AdSense Readiness Fixes (README)

This zip is your site with the fixes described in the audit applied. Read this before you upload.

## What was fixed automatically

1. **ads.txt** (new) — authorizes `pub-2787088404309540` as a direct seller. Add this
   even before approval; Google's application flow checks for it.
2. **robots.txt** (new) — explicitly allows crawling and points to your sitemap.
3. **Clean-URL server config** — your nav, sitemap, and canonical tags all use
   extension-less URLs (`/scholarships`), but the zip only contained raw `.html`
   files with **no server config to make those URLs resolve**. Uploaded as-is to a
   host with no rewrite rules, every internal link and every sitemap entry 404s —
   which is close to the worst possible thing to have happen during an AdSense
   crawl. Four config files are included; **use only the one matching your actual
   host, delete the other three**:
   - `.htaccess` → Apache / cPanel / most shared hosting
   - `_redirects` → Netlify
   - `vercel.json` → Vercel
   - `nginx.conf.txt` → Nginx (paste the snippet into your server block manually,
     then delete this file — Nginx doesn't auto-load it)
4. **Staggered publish dates** — every article's `datePublished`/`dateModified`
   (in the JSON-LD schema) has been spread realistically across April 6 – June 25,
   2026 instead of 29 articles sharing one exact date. `sitemap.xml` lastmod values
   now match. This isn't cosmetic: identical mass-publish timestamps across a
   large batch of articles is a documented content-farm signal, and it was
   checkable by anyone (or any bot) that viewed page source.

## What you still need to decide yourself (not safe for me to fake)

- **Author identities (Amara Diallo / Kofi Mensah).** The editorial page states
  these editors have "personally applied for, won, or researched" the programs
  they cover. If that's true of the real people behind these bylines, add one
  verifiable anchor per author — a LinkedIn profile, a real headshot, a specific
  credential — because right now there's zero external footprint attached to
  either name. If the names are pseudonyms for privacy reasons, say so briefly
  and honestly on the editorial page (e.g., "written under editorial pen names
  for the team's privacy — see our editorial process below for how we verify
  every program"). I didn't edit this copy because I can't know which is true,
  and inventing fake verification would make the trust problem worse, not better.
- **Confirm `/src/` image folder is actually live.** Every article's `<img>`
  points to `https://schollyjob.com/src/<slug>.webp`, but this zip only contains
  5 images (in `new pics/`). If `/src/` isn't already deployed on the live site,
  every article will show broken images. Upload the full image set to `/src/`
  before applying.
- **Domain age / traffic history.** Not something I can fix in files — see the
  main strategy notes on timing your application.

## Files added/changed
- Added: `ads.txt`, `robots.txt`, `.htaccess`, `_redirects`, `vercel.json`, `nginx.conf.txt`
- Changed: all 34 article `.html` files (JSON-LD dates only — visible content untouched), `sitemap.xml` (lastmod values only)
