# Dejana Ikonic — Landing Page

Single-file HTML + an `assets/` folder. Drops straight onto Hostinger or GitHub Pages, no build step.

```
index.html          ← the page (monogram + hero poster inlined as base64)
assets/
  hero-1920.mp4     ← 1080p hero loop, 8.0 MB  (desktop)
  hero-1280.mp4     ← 720p hero loop, 2.6 MB   (mobile)
  hero-poster.jpg   ← first-frame poster / OG image
  monogram.png      ← DI monogram, white keyed out to real alpha, 861×1002
  favicon-180.png   ← apple-touch-icon
```

## The video

Your Dropbox file is **375 MB, 4K, 59 s** — unusable as a web hero. I pulled the strongest
21 seconds (0:38–0:59, the Waterway stretch with the private docks, boat lifts and pools) and
re-encoded it two ways. Total hero payload is now ~8 MB desktop / ~2.6 MB mobile, `faststart`,
muted, looping.

Command used, if you want a different segment:

```bash
ffmpeg -ss 38 -t 21 -i source.mp4 -an \
  -vf "scale=1920:-2,format=yuv420p" \
  -c:v libx264 -preset slow -crf 26 -movflags +faststart hero-1920.mp4
```

## Config — one block, bottom of index.html

```js
const CONFIG = {
  ga4:             "",   // G-XXXXXXXXXX
  googleReviewUrl: "",   // https://g.page/r/…/review
  leadEndpoint:    "",   // Zapier catch hook or Firebase function
  fallbackEmail:   "dejanaikonic@seacoastrealty.com"
};
```

Until `leadEndpoint` is set, the form falls back to a prefilled `mailto:` — it never silently
drops a lead. Honeypot field, UTM capture and referrer are already wired into the payload.

Also in `<head>`: `google-site-verification` meta for Search Console.

## Placeholders that must be filled before this goes live

| Where | What |
|---|---|
| `#advisor` | Portrait — `assets/dejana-portrait.jpg`, 4:5, 1600×2000. Placeholder frame is in place. |
| Footer | `REPLACE_LICENSE_NUMBER` — her SC license number |
| Footer | `REPLACE_WITH_CBSCA_APPROVED_FRANCHISE_DISCLAIMER` — CBSCA has required franchise language; use theirs verbatim |
| JSON-LD | `REPLACE_GOOGLE_BUSINESS_PROFILE_URL` |
| `<head>` | `REPLACE_WITH_GSC_TOKEN`, canonical + OG URLs (currently `dejanaikonic.com`) |

## Google

I can't link her account from here — that needs her password, and I won't handle those.
What she needs to do, in this order:

1. **Google Business Profile** — create/claim it as a *Service area business* (agents can't use the
   brokerage address as their own storefront). Once verified, grab the short review link from
   Profile → Ask for reviews, and paste it into `CONFIG.googleReviewUrl` and the JSON-LD `sameAs`.
2. **Search Console** — add `dejanaikonic.com` as a domain property, take the HTML-tag token, paste
   into the meta in `<head>`. Which Google account holds it is worth deciding now — your
   `triskopedigital@gmail.com` ops account keeps it manageable if you're the one maintaining it;
   her own account is cleaner if she ever leaves.
3. **GA4** — new property, paste the measurement ID into `CONFIG.ga4`. `generate_lead`,
   `contact_call`, `contact_email` and `google_review_click` events are already firing.

The JSON-LD `RealEstateAgent` block is the piece that actually does work for her in search — it
declares the four languages, the office address and the communities, and it's the thing most agent
sites on the Strand don't have.

## One honest note on positioning

You asked for Louis Vuitton / Hermès. The page is built to that register — Bodoni, wide-tracked
caps, one script signature, gold hairlines, nothing bright, no card grids.

But the public record doesn't back it yet. Zillow shows 7 total sales, a $170K–$799K band and a
$404K average. If a $1.5M waterfront seller checks her before the listing appointment — and they do —
the gap between the page and the data reads badly.

Two ways through:

- **Lead with the language advantage.** Four languages into the Balkan/European second-home buyer
  pool is a real, defensible, uncommon edge, and it's what I built the copy around. It carries
  luxury without claiming a price band she hasn't sold into yet.
- **Fix the data trail.** Zillow shows zero reviews. Seven closings' worth of clients is seven
  reviews she doesn't have. That's the cheapest, fastest thing on this list.

Also: the copy currently says *individual listing leader, Grand Strand North, February 2026* —
that's from the CBSCA announcement and it's real. I did **not** claim CLHMS, Global Luxury Property
Specialist, or any designation. If she's earned one, tell me and I'll add it; if not, leave it out,
because those are verifiable and buyers at that level verify.
