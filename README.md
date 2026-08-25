# Carolina Waterway Plantation — Community Landing Page

A community lead-generation page for Carolina Waterway Plantation (gated ICW community,
Carolina Forest, Myrtle Beach SC), with Dejana Ikonic as the representing advisor.

Single-file HTML plus `assets/`. No build step. Deployed via GitHub Pages.

```
index.html          ← 35 KB, assets referenced as files (not base64)
assets/
  hero-1920.mp4     ← 1080p CWP aerial loop, 8.0 MB (desktop)
  hero-1280.mp4     ← 720p, 2.6 MB (mobile)
  hero-poster.jpg   ← poster / OG image
  monogram.png      ← DI monogram, white keyed to alpha, 861×1002
  favicon-180.png
```

## Page architecture

Hero (the community) → fact strip → the community → **on the water** → homes →
location & schools → Dejana as advisor → enquiry form → contact.

The water section is the conversion argument: most Grand Strand communities sell a water
*view*; this one sells a boat *launch*. Two private ramps, a community day dock, and fenced
boat/RV storage inside the gate.

## Config — one block at the bottom of index.html

```js
const CONFIG = {
  ga4:             "",   // G-XXXXXXXXXX
  googleReviewUrl: "",   // https://g.page/r/…/review
  leadEndpoint:    "",   // Zapier catch hook or Firebase function
  fallbackEmail:   "dejanaikonic@seacoastrealty.com"
};
```

Until `leadEndpoint` is set the form falls back to a prefilled `mailto:` — it never silently
drops a lead. Honeypot, UTM capture, referrer and a `community` tag are already in the payload,
so leads from this page segment cleanly if you build more community pages on the same hook.

## Placeholders to fill before promoting this

| Where | What |
|---|---|
| `<head>` | `REPLACE_WITH_GSC_TOKEN`; canonical + OG URLs if a custom domain is added |
| Footer | `REPLACE_LICENSE_NUMBER` — her SC license number |
| Footer | `REPLACE_WITH_CBSCA_APPROVED_FRANCHISE_DISCLAIMER` — use CBSCA's exact language |
| JSON-LD | `REPLACE_GOOGLE_BUSINESS_PROFILE_URL` |

## Facts on the page — verify before promoting

Sourced from public listing and community sites, not from the HOA:

- ~100 custom home sites; development began early 2000s, first homes 2004
- Private boat ramp (two launches cited), community day dock, fenced boat/RV storage
- Pool, clubhouse, tennis courts, waterfront gazebo, playground, gated entry
- HOA ≈ **$105/month** — *oldest figure on the page, from a 2023 source.* Management contact
  cited as Litus, (843) 448-9000. **Confirm the current number before this goes in an ad.**
- Zoned River Oaks Elementary / Ocean Bay Middle / Carolina Forest High — verify with Horry
  County Schools, attendance lines move
- ~6 miles to the Atlantic; off River Oaks Drive near World Tour Golf Resort

No price band is printed on the page by design — a figure in HTML goes stale in a season and
then works against her. The page routes price questions to a current market report instead,
which is also the better lead capture.

The footer carries a disclaimer that this is an independent community guide, not an HOA
publication. Keep it. Community pages that read as official draw complaints.

## Video

Source was 375 MB / 4K / 59 s. The page uses 0:38–0:59 — the Waterway stretch with the private
docks, boat lifts and pools. Re-encode a different segment with:

```bash
ffmpeg -ss 38 -t 21 -i source.mp4 -an \
  -vf "scale=1920:-2,format=yuv420p" \
  -c:v libx264 -preset slow -crf 26 -movflags +faststart hero-1920.mp4
```

Note: ffmpeg is not currently installed on this machine.
