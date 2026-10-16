# Fresh-Mill Finder — Launch Plan (draft, 2026-10-16)

## 1. Domain options (checked 2026-10-16 via registry RDAP; nothing bought)
A 404 "not found" from the registry's RDAP server means no one has registered the name. Check again right before you buy.

| Domain | Status | Notes |
|---|---|---|
| **freshmillfinder.com** | Available | Exact brand match. First choice. |
| findafreshmill.com | Available | Reads like an action, good for ads and social. |
| stonegroundmap.com | Available | Describes the product. Works if the brand changes. |
| freshmillfinder.org | Available | Buy it with the .com to protect the name. |
| localflourmills.com | Available | Plain, search-friendly name. |
| freshmills.org | Available | Short. |

A .com costs about $10–12 a year at Cloudflare Registrar or Porkbun. That is a future cost; nothing has been spent.

## 2. Stack (static, free hosting)
- **Data:** `mills.csv` is the single source of truth. A small build script turns it into `mills.json` plus one page per mill and one page per state.
- **Site generator:** Eleventy (11ty). Free, simple, outputs plain HTML. You could also skip the generator and use plain HTML/JS with the JSON file.
- **Map:** Leaflet.js with OpenStreetMap tiles. Free, no API key. Add marker clustering. Get coordinates once by geocoding city and state with OSM Nominatim, respecting its rate limits.
- **Search and filters:** client-side JS over `mills.json`. Filter by state, grain, ships, and online shop. Add Pagefind for full-text search if needed.
- **Hosting:** GitHub Pages or Cloudflare Pages. Both are free, include HTTPS, and support a custom domain. Each needs a free account, which Wendy creates herself. None was made here.
- **Forms:** "Suggest a mill / correction" and "Get featured" through a free form service (Tally, or a Google Form) until there is enough traffic to justify more.
- **Analytics:** Cloudflare Web Analytics (free, no cookies) or GoatCounter.

## 3. Newsletter (free tier)
- **Recommended: Kit (formerly ConvertKit).** The free plan covers a large list (about 10k subscribers at last check; confirm before signing up), with embeddable forms and tags such as "ships nationwide fans" or by state.
- **Alternatives:** beehiiv free plan, which has a built-in referral and ad network later, or Buttondown, which is minimal and markdown-friendly but has a small free cap.
- **Format:** a weekly "Mill of the Week" spotlight, 3 new or updated listings, one recipe that uses a featured flour, and one affiliate pick (King Arthur via Awin, Challenger Breadware). Label the affiliate links.

## 4. Site pages
1. **Home:** map, search bar, quick filters (Ships nationwide, Shop online, Heritage/ancient grains), newsletter signup.
2. **Directory:** a filterable list/table view of all mills.
3. **State pages** (`/state/vt/` and so on): good for SEO ("flour mills in Vermont").
4. **Grain pages** (`/grain/einkorn/`, `/grain/rye/`, `/grain/sonora-wheat/`, and more).
5. **Mill detail pages:** what they mill, where they are, whether they ship, a "Shop" link, last-verified date, and a "suggest an edit" link.
6. **Ships Nationwide:** a curated list. This is the highest-intent page.
7. **Guides:** "What is stone-ground flour", "Storing fresh flour", "Starter kit". This is where the affiliate links go.
8. **Newsletter** signup and archive.
9. **For Mills:** claim or update a listing, plus featured listing pricing.
10. **About / Methodology / Sources:** credit the Whole Grains Council map, Sourdough Geeks, Amy Halloran, Grinder Finder, and Tufts.
11. **Legal:** affiliate disclosure (FTC) and privacy policy.

## 5. Monetization notes
- **Featured listings:** start with a low flat price (for example $10–25/mo or $99/yr): pin to the top of the state page, badge on the map, one newsletter mention per quarter. Sell after the site has traffic.
- **Affiliates:** King Arthur (Awin, 5%) and Challenger Breadware (10%). Put them in guides and gear lists, not on mill listings, to keep the listings neutral.

## 6. Launch checklist
- [ ] Clean the data: confirm each mill's city and the ships and retail-online flags (see the data caveats in the README section below). Geocode.
- [ ] Re-check the ~70 candidate mills whose sites failed from our network (list in `raw/checked2.json`). Many are likely live.
- [ ] Buy freshmillfinder.com (plus the .org if wanted).
- [ ] Create free GitHub and Cloudflare accounts. Deploy the static site and point the domain at it.
- [ ] Add the Kit signup form and send a welcome email.
- [ ] Apply to Awin (King Arthur) and the Challenger affiliate program. Add the disclosure page.
- [ ] Publish the About/Sources, Privacy, and Affiliate disclosure pages.
- [ ] Submit the sitemap to Google Search Console and Bing Webmaster Tools.
- [ ] Email or DM mills to say they're listed and invite them to claim or correct their listing. Only Wendy sends these, after she approves.
- [ ] Post the launch in baking communities (r/Breadit, sourdough groups, Instagram) and with grain alliances.
- [ ] Re-verify all listings every quarter and update the `last_verified` field.

## Data caveats (mills.csv)
- 148 mills, farms, and milling bakeries in 41 states plus DC. Every website loaded (HTTP 200) on 2026-10-16 and its homepage mentioned flour, grain, or milling. Hijacked or dead domains were dropped, along with industrial-scale millers (Ardent, Bay State, ND Mill, and others).
- `grains_flours` comes from the WGC map where it had the mill. Otherwise it lists grain words that appeared on the mill's homepage. Spot-check it.
- `ships=yes` only where the site's shipping text was seen or WGC lists Mail Order. A blank means unknown, not no.
- `sells_retail_online=y` means an online shop or cart was detected on the homepage (an automated signal). A blank means not detected.
- `city` is blank for many mills from the Sourdough Geeks source, which lists only the state.
