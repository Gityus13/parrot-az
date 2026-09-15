# PARROT-AZ — deploying to GitHub Pages

This folder is a ready-to-push GitHub Pages site for **parrotaz.site**.

## What's in here

| File | Purpose |
|---|---|
| `index.html` | The site itself (SEO tags, canonical URL, Open Graph/Twitter cards already point at `https://parrotaz.site/`) |
| `CNAME` | Tells GitHub Pages to serve this repo on your custom domain |
| `robots.txt` | Allows all crawlers, points to the sitemap |
| `sitemap.xml` | Single-page sitemap for `https://parrotaz.site/` |
| `site.webmanifest` | Makes the site installable (PWA-style "Add to Home Screen") |
| `404.html` | Styled not-found page GitHub Pages serves automatically for bad URLs |
| `.nojekyll` | Stops GitHub's Jekyll build step from touching the files (not needed here, but a safe default) |
| `icons/` | favicon.ico, PNG icons (192/512), apple-touch-icon, and the 1200×630 `og-image.png` used for social share previews |

## 1. Push it to a repo

This is a **project page** (not a `username.github.io` repo), so it can live in any
repo, e.g. `parrot-az`:

```bash
cd path/to/this/folder
git init
git add .
git commit -m "Initial site"
git branch -M main
git remote add origin https://github.com/Gityus13/parrot-az.git
git push -u origin main
```

## 2. Turn on GitHub Pages

1. On GitHub: repo → **Settings** → **Pages**.
2. Under **Build and deployment**, set **Source** to "Deploy from a branch".
3. Branch: `main`, folder: `/ (root)`. Save.
4. GitHub will build the site at `https://gityus13.github.io/parrot-az/` first —
   that's expected and temporary.

## 3. Point your domain at it (parrotaz.site)

The `CNAME` file in this repo already contains `parrotaz.site`, so GitHub knows
which domain to expect. You still need to point the domain's DNS at GitHub:

**At your domain registrar / DNS provider, add these records** (apex domain, so `A` records, not `CNAME`, since `parrotaz.site` has no subdomain prefix):

| Type | Host | Value |
|---|---|---|
| A | @ | 185.199.108.153 |
| A | @ | 185.199.109.153 |
| A | @ | 185.199.110.153 |
| A | @ | 185.199.111.153 |

Optional but recommended — also add a `www` redirect:

| Type | Host | Value |
|---|---|---|
| CNAME | www | gityus13.github.io |

(If you'd rather use `www.parrotaz.site` as the primary domain instead of the
apex, swap this around: `CNAME` record for `www` pointing at
`gityus13.github.io`, and change the contents of `CNAME` in this repo to
`www.parrotaz.site`.)

DNS propagation can take a few minutes to a few hours.

## 4. Enforce HTTPS

Back in **Settings → Pages**, once GitHub detects the DNS is correct (may take
a bit), a **Custom domain** field will show `parrotaz.site` with a green
checkmark. Tick **Enforce HTTPS** once it becomes available (GitHub needs to
issue a certificate first — can take up to ~24h after DNS is live).

## 5. Verify

Once it's live, double check:

- `https://parrotaz.site/` loads the site
- `https://parrotaz.site/robots.txt` and `https://parrotaz.site/sitemap.xml` load
- `https://parrotaz.site/nonexistent-page` shows the styled 404
- Paste `https://parrotaz.site/` into a [Facebook Sharing
  Debugger](https://developers.facebook.com/tools/debug/) or [Twitter Card
  Validator](https://cards-dev.twitter.com/validator)-style checker to confirm
  the `og-image.png` preview renders

## Notes

- If you ever rename the repo or switch to a `username.github.io` user-page
  repo instead, nothing here changes — the `CNAME` file and the URLs baked
  into `index.html`/`robots.txt`/`sitemap.xml` are all based on the domain,
  not the repo name.
- If you later drop the custom domain and just want the default
  `github.io` URL, delete `CNAME` and run a find/replace across `index.html`,
  `robots.txt`, and `sitemap.xml` swapping `https://parrotaz.site/` for your
  `https://USERNAME.github.io/REPO-NAME/` URL.
