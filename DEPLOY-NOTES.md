# ADHD & Her — new home: deploy notes

Two folders. Nothing here touches Kajabi. Kajabi stays live until buyers have been emailed and the new pages are tested.

## 1. `tools-repo/` → add to the existing repo `lgreenshelley/adhd-and-her-tools`

Copy the contents of `tools-repo/` into the repo root (it adds `access/` and `robots.txt`, and replaces two existing files):

| Path | What |
|---|---|
| `access/hs-prep-p9x3wn/index.html` | Buyer page: Preparing Your ADHD Tween for High School |
| `access/regulation-toolkit-4k7mq2/index.html` | Buyer page: My Regulation Toolkit, Teen Girls |
| `access/sensory-blueprint-t2h8vc/index.html` | Buyer page: My Sensory Blueprint, Women's |
| `access/files/` | Drop the course PDFs here — see `README.txt` inside for exact filenames |
| `robots.txt` | Tells search engines to ignore `/access/` |
| `regulation-checkin/index.html` | **Replaces existing.** The six "buy the course" CTAs now say courses are paused and link to Instagram; dead `shop.` links removed |
| `hs-readiness-screener/index.html` | **Replaces existing.** Two links to Kajabi pages now point to the home page |

Then commit and push. Pages go live at `https://tools.adhdandher.com.au/access/<slug>/` within a minute or two.

**Videos:** the pages currently show a "being moved to new hosting" placeholder in each video slot. Once the Bunny embed IDs are in, I regenerate the three pages and you push again. Nothing else changes.

## 2. `site-repo/` → a NEW repo for the main domain

GitHub Pages allows one custom domain per repo, and the tools repo already uses `tools.adhdandher.com.au`, so the main site needs its own repo.

1. On GitHub: New repository → name it `adhdandher-site` → Public → Create.
2. Upload everything inside `site-repo/` (including the hidden `.nojekyll` and `CNAME`).
3. Repo Settings → Pages → Source: "Deploy from a branch", branch `main`, folder `/ (root)` → Save. Custom domain should auto-fill `www.adhdandher.com.au` from the CNAME file. Tick "Enforce HTTPS" once it's available (can take up to an hour after DNS).

### DNS (GoDaddy) — do this only after step 2 is live

Delete the existing records Kajabi asked you to add for `www` and `@`, then add:

| Type | Name | Value |
|---|---|---|
| CNAME | `www` | `lgreenshelley.github.io` |
| A | `@` | `185.199.108.153` |
| A | `@` | `185.199.109.153` |
| A | `@` | `185.199.110.153` |
| A | `@` | `185.199.111.153` |

Leave the `tools` CNAME exactly as it is. Leave all MX / email records exactly as they are.

Once DNS moves, `www.adhdandher.com.au` shows the holding page and Kajabi's copy of the site is unreachable — so this is the last step, after the buyer email has gone out.

### Stripe buy buttons

All four Buy buttons point at the live Stripe Payment Links (ADHD and Her Stripe account, created 4 Sept 2026). To change a link later, edit `stripe.json` and re-run `gen_sales.py`.

### Images

`images/README.txt` lists the six image files to save into `images/`. Pages render without them.

### What the site contains

| Path | What |
|---|---|
| `/` | Home: four product cards with prices, free check-in, about, FAQ |
| `/regulation-toolkit-teens/`, `/adhd-tween-high-school/`, `/sensory-blueprint-women/`, `/high-school-readiness-screener/` | Sales pages, ported from the Kajabi copy, with Stripe Buy buttons |
| `/terms/`, `/privacy/` | Terms & refunds, privacy policy (from Kajabi) |
| `/links/` | Link in Bio — set this as the Instagram bio link |
| `/link-in-bio/`, `/work-with-me/`, `/tools-and-courses/`, `/my-story/`, `/contact/`, `/high-school-heads-up/` | Redirects to `/` so old Kajabi URLs (and the screener's built-in links) don't 404 |
| `/free-check-in/`, `/free-reg-check-in-adhd-girls/` | Redirect to the free tool |
| `404.html` | Friendly not-found page for everything else |

Images: the old logo, headshots and product mockups were hosted on Squarespace/Kajabi CDNs and will vanish when those close. Save the six files listed in `images/README.txt` into `images/` before then.
