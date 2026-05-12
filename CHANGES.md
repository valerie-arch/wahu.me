# Wahu site rewrite — change log

---

## Pass 3 delta (May 2026 site-diagnosis memo applied)

### CRITICAL — pricing cadence + math
- **GHS 420 / month → GHS 420 / week** site-wide (it was wrong; weekly is the real cadence). Affected: homepage hero CTA + final CTA, vehicles hero CTA + configurator step 03 + pricing strip + final CTA + compare table, footer link copy.
- **Configurator math recalculated**: `78 weekly payments × GHS 420 = GHS 32,760 paid in over 18 months` (was understated by ~GHS 25,200).
- Configurator strip rewritten to: `Bundles bike, service, insurance, training, app and warranty · Bike yours at the end of week 78`.
- Compare table on homepage now lists `From GHS 420 / wk` and the eMoto reads `Join the waitlist`.

### NEW — 24-month TCO stacked-bar chart
- Built a CSS-only horizontal stacked-bar chart matching the memo's spec exactly:
  - Petrol bar = GHS 48,520 total (Bike 13,000 · Fuel 29,120 · Service 4,800 · Insurance 600 · Training 1,000)
  - Wahu bar = GHS 36,400 total (Bike + service + insurance + training + app + warranty 32,760 · Charging 3,640)
  - Petrol bar width = 100%, Wahu bar = 75.02% — the visual ratio matches the cost ratio
  - Caption: "GHS 36,400 vs GHS 48,520 over 24 months — a saving of GHS 12,120, plus you keep GHS 13,000 in your pocket on day one. Wahu bundles service, insurance and rider training; petrol bikes don't."
- Section sits as a dedicated `<section class="tco-band" id="tco">` immediately after the homepage hero, and is **embedded again on `vehicles.html`** between the compare table and the charging section.
- Petrol segments use muted earthy reds (`#5C5E62 → #AC745F`); Wahu segments use `var(--ink)` + `var(--accent)` orange.
- Mobile: stacked label/bar, 56px bar height, condensed labels.

### Homepage copy + structure
- Hero subhead: "Cheaper to run than a petrol bike. And after 18 months, it's yours." (replaces broken "week of petrol" analogy).
- Final-CTA subhead: "From GHS 420 a week. ~25% cheaper than petrol over 24 months. Yours after 18." Duplicated-phrase bug fixed.
- Hero eyebrow: "Designed in Ghana · Built for everyone" → "Designed in Ghana · Built for the people who ride every day".
- Testimonial eyebrow: "A WAHU HERO" → "FROM A RIDER IN ACCRA".
- **Compare table expanded** with bike-payment + insurance + training rows so Wahu's column reads `Included × 4`.
- **NEW: FAQ section** (`<section class="faq-band">`) with 6 native `<details>` accordions covering price, savings, what-happens-after-18-months, charging, what's-included, sign-up. Wired with `FAQPage` JSON-LD schema.

### Vehicles copy
- "Daily driver of the new African city" → "Daily driver" (drop the redundant tail).
- eMoto headline + tag: "Built to conquer. Forged to endure." → "Built for 200km days. Pays for itself in a year." (in both showcase and detail h2).
- TCO chart embedded between compare table and charging.

### Business H1 + supporting copy
- H1: "Lower your fleet's TCO. Recover late payments. Move every rider to electric." → **"Run a fleet of bikes? Cut your fuel cost by 87%. Coach your fleet with Sidekick.ai."**
- Subhead replaced with: "Trusted by Bolt Food, Glovo, Jumia, Yango and Uber Eats. From 5 bikes to 5,000."
- Removed the small inline outcome chip strip (`30% lower TCO · 94% on-time payment · Zero petrol`) — those numbers now live elsewhere on the page (Sidekick / Keba.ai stats).
- Sidekick body sharpened: "Sidekick texts every rider every morning with what they need to earn more today. Riders earn 18% more. Runs on its own."
- Removed "Open APIs from day one" from feature list (per memo — move to Technical panel later, or delete).
- Added price-floor line to demo perks: "From GHS 420 / bike / week — bundles bike, charging access, software, service".

### Investors H1 + structure
- H1: "One bet. Three ways. One company." → **"Africa's first electric mobility company with a sovereign carbon contract."**
- Subhead: "Anyone can import bikes. Very few can build the operating system underneath them."
- **Self-quote attribution removed**: cut "— Wahu Mobility · Product Strategy 2025/26" line.
- **Linked chip strip** added below the thesis pull-quote (4 chips, all clickable):
  - `USD 18m sovereign carbon offtake → /impact`
  - `Six revenue streams → #ecosystem`
  - `Vertically integrated → /vehicles`
  - `African-led → #round`
- **Leadership grid moved from /careers to /investors**: full 4-person card grid (Valerie Labi · CEO, Abena Baidoo · CFO, Christopher Amewuho · Head of Tech, Quincy Agyapong · Head of Production) replaces the 3 generic placeholder team cards in the round/team merged section. Quincy's surname is correctly spelled "Agyapong" throughout.

### Careers cuts
- **Five-values block deleted** entirely (Caring Passionately / Bold Champions / Inclusive / Resourceful / Trustworthy) — kept internal per memo.
- "We are philomaths" → "We learn obsessively" (with body shortened accordingly).
- **Leadership grid slimmed**: 4 minimal avatar cards (name + role only, no bios) with a "See the full leadership grid →" link to `/investors#round`.

### Impact rewrite — cut and reorder
- Cut from ~1,463 words to ~800. Sections deleted: "01 People (Lives lifted)" and "03 Path to ownership (From renter to owner)". The Kwabena Asante quote was duplicated across them and the second contradicted the first — kept neither, since the climate funder audience doesn't need rider testimonials repeated.
- **New section order**: 01 Verified at the cell, not estimated · 02 From rider to recorded · 03 Women on the road · 04 Talent & partnerships. Each has a fresh eyebrow.
- Section 01 "Planet" was renamed and **expanded with the Article 6.2 / KliK Foundation detail** (now a section header, not a parenthetical sentence): "Africa's first sovereign-backed carbon contract on two wheels. Ghana's Letter of Authorisation backs the contract; Switzerland's KliK Foundation is the offtake partner. Sovereign-backed, audit-grade, ride-level."
- Section 04 Talent & Partnerships condensed (UKBIC paragraph kept, redundant academic-ecosystem sentence trimmed).
- Phrase changes: "owning what they ride" → "owning the bike"; "the cruel paradox of the gig economy" → "the paradox of the gig economy"; "sovereign-backed, audit-grade, real" → "sovereign-backed, audit-grade, ride-level".
- Commitments band already moved to position 3 (between manifesto and themes) in pass 2 — kept there.

### SEO infrastructure (every page)
- **Canonical tags** on all 6 pages pointing at `https://wahu.me/{path}`.
- **og:image / og:url / og:type / og:locale / og:site_name** + image dimensions (1200×630). Default OG image is `assets/brand/emoto-arch.jpg` (the Independence Arch eMoto hero — the most recognizable Wahu shot).
- **Twitter Cards**: `summary_large_image` with title/description/image per page.
- **theme-color** meta = `#171A20` (matches `--ink`).
- **JSON-LD schemas** injected per page:
  - `Organization` (sitewide) — name, url, logo, founder location, sameAs links to LinkedIn/Instagram/Facebook, three contact points (hello / investors / careers).
  - `LocalBusiness` (homepage) — Accra address, telephone, priceRange "GHS 420 / week".
  - `WebSite` (homepage).
  - `FAQPage` (homepage) — all 6 questions/answers as `Question`/`Answer` objects.
  - `Product` × 2 (vehicles) — eBike (`Offer` with priceCurrency GHS, price 420, weekly `unitCode WEE`, InStock); eMoto (`Offer` PreOrder, no price).
  - `VideoObject` (investors) — founder video metadata.
- All schema is wrapped in a single SEO block at the bottom of each `<head>` so it can be regenerated by re-running the injector if metadata ever changes.

### sitemap.xml + robots.txt
- `sitemap.xml` at project root with all 6 URLs, lastmod `2026-05-09`, weekly/monthly changefreq, priorities 1.0 → 0.6, plus `image:image` entries for the homepage hero and the eBike product shot.
- `robots.txt` allows all crawlers, disallows `/rider/` (separate rider app), points to `https://wahu.me/sitemap.xml`.

### What's still TODO (deferred from the memo)
- **Days 8–30**: build /accra, /tema, /kumasi city landing pages; build /rent-to-own; build /financing.
- **Days 61–90**: pitch the Article 6.2 / KliK story to Bloomberg Africa, Climate Home News, Reuters Africa; publish methodology paper "How Wahu measures carbon at the cell"; get listed in Crunchbase / Briter Bridges / AfriLabs / Disrupt Africa / GSMA Innovation Fund alumni; quarterly impact report at `/impact/q3-2026`.
- **Imagery**: original phone-in-hand photo (file at `assets/hero-app.jpg` is currently the riders-line photo; needs the original re-exported).
- **Insurance number**: chart uses GHS 600 / 2yr (third-party legal minimum). Memo recommends staying conservative — keep as-is until comprehensive figure is confirmed by Abena.
- **20-second screen-record demo of the dashboard** for `/business` (asset to be produced).
- **Calendly URL** wired into investors sequential CTA — currently placeholder `https://calendly.com/wahu-investors`.
- **Plausible analytics** snippet not yet added (still recommended).



Pass executed top-to-bottom across `index.html`, `vehicles.html`, `business.html`, `impact.html`, `investors.html`, `careers.html`. CSS classes / IDs / structural patterns preserved. New components added: eBike configurator, eMoto waitlist (replaced configurator), customer logo strip, sequential data-room CTA, real Wahu wordmark logo in nav + footer.

---

## Pass 2 delta (post-review fixes)

### Real prices + waitlist
- **eBike pricing** — `GHS 280 / week` placeholder replaced site-wide with confirmed `GHS 420 / month`. Affected: hero CTA on `index.html` + `vehicles.html`, final CTA on both, eBike configurator step 03 + pricing strip, compare table on `vehicles.html`. Math line on the configurator pricing strip recalculated: `From GHS 420 / month · 18 monthly payments × GHS 420 = GHS 7,560 paid in · Includes service, insurance, and the Hero app · Bike yours at the end of month 18`.
- **eMoto pricing → waitlist** — eMoto isn't priced yet. The eMoto configurator section was rewritten as a waitlist block: headline `Join the eMoto waitlist.` + eyebrow `COMING SOON`. Three info cards (Built for working riders / Battery swap network / Direct platform integration) replace the colour/battery/pay-weekly steps. An inline waitlist form (name, email, city) replaces the pricing strip; on submit it shows a "you're on the list" confirmation. eMoto CTAs everywhere (homepage tile + vehicles eMoto showcase) now read `Join the waitlist →` and anchor to the new form. Compare-table row renamed `Pricing`: `From GHS 420 / month` (eBike) vs `Join the waitlist` (eMoto).

### New eMoto photography
- Two new product shots saved to `assets/brand/`:
  - `emoto-arch.jpg` — single rider on the eMoto in front of Independence Arch, Accra. Now the full-bleed photo on the vehicles-page eMoto showcase (replaces `assets/emoto-action.jpg`).
  - `emoto-street.jpg` — two riders on the eMoto in a city street. Now the homepage eMoto tile photo (replaces `assets/emoto-action.jpg`).
- Old `assets/emoto-action.jpg` (delivery rider with green box) is no longer referenced from the live site but kept on disk in case it's wanted later.

### Hero contrast — white text legibility
- The hero gradient was too soft on lifestyle photography (mid-tones eating the white headline). Replaced with a stronger 4-stop ramp on every hero across all 6 pages: `linear-gradient(180deg, rgba(0,0,0,.55) 0%, rgba(0,0,0,.35) 35%, rgba(0,0,0,.4) 65%, rgba(0,0,0,.7) 100%)`. Top of hero (where the headline lives) is now ~55% black overlay; bottom (where the buttons live) is ~70%. Same treatment applied to the homepage tile-shade (top + bottom darker) so the eyebrow / headline / body / button stack on each tile reads against any underlying photo.

### Real Wahu logo (replaces text wordmark)
- Brand wordmark `Wahu` (text) replaced with the actual `wahu!` logo PNG (`assets/brand/wahu-logo-rgb.png`) in:
  - the nav `.brand` lockup on every page
  - the footer `.foot-brand` lockup on every page
- New CSS rules added inline on each page: `.brand-mark{height:22px;width:auto;display:block;transition:filter .3s}` + `.nav.over-hero .brand-mark{filter:brightness(0) invert(1)}` so the dark-ink logo flips to white when the nav is sitting over a hero photo, and back to dark navy when the nav becomes white-on-scroll. Footer logo stays dark navy on the white footer background. `.foot-brand-mark{height:14px}` for the smaller footer placement. No second white asset needed — the CSS filter does it cleanly without an extra file.

### Other fixes
- **Quincy Agyapon → Quincy Agyapong** on `careers.html` leadership card (TODO #3 closed).

---

## Per-file changes

### index.html
- **Hero** — rewrote lede to "From GHS 280 a week — the same weekly cost as petrol — and after 18 months the bike is yours. Riding for delivery, ride-hail, or to work and back." Replaced button pair with one primary `Order from GHS 280 / week` + secondary text link `See the vehicles →`.
- **DELETED** the duplicate "Two vehicles. One way to ride." video block that immediately followed the tile grid (overlapped the section header, doubled as a play-card by rule 1.2).
- **DELETED** the offers-section (two off-ramp cards: "Spend less. Earn more." + "Your bike. Your phone. Your business.") — the doc's "Three off-ramp cards (DELETE)" maps to these in the redesigned page; both repeat content shown later.
- **Tile grid (eBike + eMoto)** — added a new section header above the grid: eyebrow `THE VEHICLES` / h2 `Two vehicles. One way to ride.` / lede `eBike for everyday riding. eMoto for working riders. Both pay for themselves. Both are yours after 18 months.` Each tile now has eyebrow ("For everyday riding" / "For working riders"), name, body line, spec row, and ONE button (`Configure & order →`) anchoring to the matching configurator on `/vehicles`.
- **Compare ("Spend less. Earn more.")** — kept as-is per doc.
- **DELETED** the steps band ("How it works / From signing up to riding away") — moved to `vehicles.html` per doc Section 5.
- **App tile** — rewrote lede to "Track your battery, your earnings, and how close you are to owning your bike — every day, in your pocket. Free with every Wahu." Six-feature list and store buttons retained.
- **DELETED** the Hero stories video block ("Watch the way Wahu changes a working day").
- **Testimonials** — cut from 3 quotes to 1 (kept Kwabena A. · Delivery rider · Accra). Eyebrow → `A WAHU HERO`. Headline → "One quote, from one rider." Card sized up.
- **Off-ramp two-card row (Impact / Business)** — bodies tightened: Impact card → "2.4 tonnes of CO₂ avoided per rider per year. Verified by telematics, not estimated." (CTA: `See the impact →`). Business card → "One screen. Every bike. Every payment. From 5 bikes to 5,000." (CTA: `See fleet solutions →`).
- **Final CTA** — rewrote lede to "From GHS 280 a week. Yours after 18 months. Same weekly spend as petrol — only this time, the bike ends up yours." Replaced button pair with one primary `Order from GHS 280 / week` + secondary text link `For business →`.

### vehicles.html
- **Hero** — kept as-is. Replaced button pair with one primary `Order from GHS 280 / week` + secondary text link `Compare eBike vs eMoto →` anchoring to the comparison section.
- **MOVED** the comparison table up — it now sits between the hero and the eBike showcase (Tesla "pick a model first" pattern). Lede rewritten: "eBike for everyday. eMoto for work. Pick the one that fits the kind of riding you do." Added a new row: `Weekly payment · From GHS 280 / From GHS 380` (accent colour).
- **eBike showcase** — bumped the four spec callouts (140 km / 40 km/h / 1000 W / 150 kg) to 40 px, 48 px gap, no chrome (already chrome-free in the base CSS — increased emphasis to match the doc's "right on the bike" treatment). Replaced `Custom order` / `Learn more` button pair with one `Configure & order →` anchoring to the new configurator.
- **eBike detail** — eyebrow / headline kept. Lede tightened: "Less sweat. More street. For everyday riding — to work, to school, around town, beating the traffic. Quiet enough for the morning. Smart enough to know how far it can go." (split the run-on sentence per doc).
- **NEW: eBike configurator** — three-step block (Pick a colour · Pick a battery · Pay weekly) on `var(--surface)` background. Pricing strip: `FROM GHS 280 / WEEK · 18 weekly payments × GHS 280 = GHS 5,040 paid in · Bike value at handover: GHS 4,800 · Difference covers service, insurance, and the Hero app`. Primary CTA `Order this build →` (mailto with subject pre-filled), secondary text link `Speak to someone first →`.
- **eMoto showcase** — same callout treatment + one `Configure & order →` button.
- **eMoto detail** — kept as-is.
- **NEW: eMoto configurator** — mirrors eBike. Colours: Matte black · Forest · Charcoal · Signal. Battery: Standard 72V (100 km) / Long-range 72V (130 km). Pay weekly: GHS 380. Pricing strip: `FROM GHS 380 / WEEK · Includes service plan · Includes unlimited battery swaps · Direct integration with Bolt, Glovo, Jumia`.
- **DELETED** the "A morning on the eMoto" video block (rule 1.2).
- **Charging** — sharpened card 1 body: "Plug in when you get home. Wake up to a full battery. GHS 35 / week to charge — vs GHS 280 for petrol. The charger ships free with every Wahu and works on any standard outlet." Cards 2 and 3 kept.
- **Ride-to-own** — added a new "Before the bike: how to sign up" four-card row (the moved-from-homepage how-it-works steps) above the existing four steps, which are now framed as "After the keys: how it ends".
- **Final CTA** — replaced button pair with one primary `Order from GHS 280 / week` (anchors to eBike configurator) + secondary text link `For business →`.

### business.html
- **Hero** — kept eyebrow. New headline: "Lower your fleet's TCO. Recover late payments. Move every rider to electric." New lede: "Wahu gives you the bikes, the charging network, and the software to run them — all from one screen. From 5 bikes to 5,000." Replaced button pair with one primary `Book a demo · Free 4-week trial` + secondary text link `See how it works →`. **Added** an inline outcome strip directly under the buttons: `30% lower TCO · 94% on-time payment · Zero petrol`.
- **DELETED** the "Five spreadsheets. Three WhatsApp groups. No answers." problems section (3-card pain-point row).
- **Dashboard feature** — eyebrow `THE DASHBOARD`, new headline "One screen. Every bike. Every payment.", new lede "See every bike, every rider, every payment in real time. Lock or unlock any bike from anywhere. Send invoices in seconds." Five-feature list and dashboard mockup card kept. Added `id="dashboard"` so the hero's text link can anchor to it.
- **MERGED** Sidekick + Keba.ai — the two full-bleed dark feature sections are now one light section with a two-card row (`AI PRODUCTS / Two AI products. Built for fleets like yours.`). Each card has eyebrow, headline, body, an outcome stat (Sidekick: `+18% rider earnings`, Keba.ai: `94% on-time payment`), and a `Learn more about X →` link. New CSS: `.ai-grid`, `.ai-card`, `.ai-stat`.
- **DELETED** the "90-second tour" video block (rule 1.2).
- **REPLACED** the four-card "Built for operators like you" grid with a customer logo strip (`Bolt Food · Glovo · Jumia · Yango · Uber Eats`). Wordmark fallback in `Manrope 500` on the surface background until logo permissions are confirmed. New CSS: `.logo-strip`. Section eyebrow `OUR OPERATORS`, headline `Trusted by the fleets moving African cities.`
- **Demo form** — removed the "Your business" field (cut from 5 to 4: name, work email, fleet size, country). Headline → `Book a demo.` Sub → `Free 4-week trial. We reply within 2 working days.` Submit button label kept (`Book a demo →`). Four perks kept.

### impact.html
- **Hero** — kept eyebrow / headline / lede. Replaced button pair with one primary `Buy carbon credits` (mailto:carbon@wahu.me) + secondary text link `See the impact →`.
- **Manifesto pull-quote** — kept as-is.
- **MOVED** the 2030 Commitments section UP to position 3 — now sits between the manifesto and the six themed sections. Lede tightened: "Numbers and dates. Ours, on the record. Quarterly progress, in the same dashboards our investors see."
- **Six themed sections (People / Planet / Path to Ownership / Financial Inclusion / Gender / Talent & Partnerships)** — kept exactly as written.
- **DELETED** the "A day with a Hero. A year of change." video block per doc Section 5 default action (cross-cutting rule 1.2).
- **Partners and verifiers** — kept as-is.
- **Final CTA (Build / Buy / Back)** — kept as-is.

### investors.html
- **Hero** — kept "One bet. Three ways. One company." Replaced button pair with one primary `Request the data room` + secondary text link `The thesis →`.
- **Thesis** — pull-quote upsized to ~1.5× (`clamp(36px, 4.5vw, 57px)`) with `padding: 100px 0` for breathing room. Below the quote: a folded inline bullet line (`Vertically integrated · Six revenue streams · Auditable impact · African-led`) and a small text link `Auditable, ride-level carbon savings — see the full impact framework →` linking to `/impact`.
- **The opportunity (4-stat row $25B / 25M / 22% / 30%)** — kept as-is.
- **DELETED** "The stack. Five layers. Six revenue streams." 5-row table (belongs in the deck).
- **Founder video** — kept as-is. This is the ONE surviving video / play-card across the whole site (rule 1.2).
- **DELETED** the "Four reasons this is a moat business" pillar grid (folded into the thesis section as inline bullets).
- **DELETED** "Every product makes the next one easier." flywheel section.
- **DELETED** "Auditable impact compounds with operational data." section (replaced by the small line at the bottom of the thesis section).
- **MERGED** "The round" + "The team" into one section: 5/12 left column (round table + pull-quote + sequential CTA) and 7/12 right column (three team cards). New CSS: `.round-merge`. Section headline changed from "Series A in active preparation." to "Series A. Open now."
- **Sequential CTA** — `Request the data room →` button is now a gate. On click it reveals an inline form (name, fund, work email, indicative ticket size). On submit, a success state shows a `Now book a call →` button pointing to `https://calendly.com/wahu-investors` (placeholder URL, see TODO #8).
- **Final CTA** — replaced button pair with one primary `investors@wahu.me` + secondary text link `See the vehicles →`.

### careers.html
- **Hero** — kept the headline. Lede shortened to "Hard work. Real impact. The chance to leave the continent better than you found it." Replaced button pair with one primary `See 8 open roles` + secondary text link `Why Wahu →`.
- **Manifesto** — kept as-is.
- **Leadership (4-card grid)** — kept as-is.
- **Why Wahu (2×2 grid)** — kept as-is.
- **DELETED** "A look inside the Wahu workshop" video block (rule 1.2).
- **Values (5-card row)** — kept as-is.
- **Open roles (8 mailto rows)** — kept as-is.
- **Don't see your role CTA** — demoted `See our impact` from a parallel button to a small text link beneath the primary `careers@wahu.me` (rule 1.3).

---

## Skipped / ambiguous decisions

- **`index.html` Section 2 — "three off-ramp cards"** — the redesigned homepage didn't have exactly three off-ramp cards. I deleted (a) the duplicate "Two vehicles. One way to ride." video-style block that immediately followed the tile grid and (b) the two-card offers section ("Spend less" + "Your bike, your phone"). Both repeated content that appears in proper detail later, which matches the spirit of the instruction.
- **`vehicles.html` spec callouts** — the doc says to "strip styling on the four spec callouts." In my redesigned base, those callouts already render as text-only (no card / border / panel). I kept the styling clean and bumped the size up to `40 px` with `48 px` gap to match the "big, sitting on the photograph" intent.
- **`vehicles.html` how-it-works move** — added the four-card row inside the existing `.own-band` section rather than as a separate `<section>`, with a small `.label`-style sub-heading "Before the bike: how to sign up" so the Ride-to-own section reads cleanly as: 1) intro, 2) before the bike, 3) after the keys. Existing 4-step `<ol>` rebadged with sub-heading "After the keys: how it ends".
- **`investors.html` Section 6 (moat pillars)** — chose "DELETE + fold into thesis" over standalone section. Bullets sit beneath the thesis pull-quote as a single line.
- **`impact.html` Section 5 — "A day with a Hero" video** — used the document's default action: DELETE.
- **`careers.html` final CTA** — applied the optional consistency tightening (rule 1.3): demoted `See our impact` to a text link.
- **CSS** — I kept all original CSS classes/IDs intact and only ADDED new rule blocks for the new components (`.cfg-band` / `.cfg-step` / `.cfg-pricing` on vehicles, `.ai-grid` / `.ai-card` / `.ai-stat` and `.logo-strip` on business, `.round-merge` on investors). No existing rules were modified.

---

## TODOs (real assets / decisions still needed)

1. **Confirm real weekly prices in GHS** for eBike and eMoto with Abena (CFO). Find-and-replace `GHS 280` and `GHS 380` placeholders site-wide. Affected files: `index.html`, `vehicles.html` (configurators + final CTA + compare table), `business.html` not affected directly. Configurator illustrative math (`18 weekly payments × GHS 280 = GHS 5,040`) also needs a real-terms rewrite — current copy notes "real terms are 18 months."
2. **Confirm real fleet outcome stats** with Christopher (Head of Tech) and Quincy (Head of Production): the `30% lower TCO · 94% on-time payment · Zero petrol` strip on `business.html`, plus the `+18% rider earnings` Sidekick stat and `94% on-time payment` Keba.ai stat. If real numbers aren't yet defensible, swap to the conservative phrasing: "Built for lower TCO, on-time payment, and full electrification."
3. **Verify spelling: Quincy Agyapon vs Agyapong** on `careers.html` (and on `investors.html` if listed there — currently the team cards on investors merged page don't name him individually, so only careers).
4. **Customer logos on `business.html`** — verify and secure permission for Bolt Food, Glovo, Jumia, Yango, Uber Eats. Current implementation is wordmark fallback in Manrope 500. Once permissions arrive, replace `<span>` text with proper SVG/PNG logos.
5. **Open roles on `careers.html`** — eight roles are placeholder titles per design. HR to confirm the live openings and adjust the list before publishing. Hero button currently reads `See 8 open roles` — update the count if the real list is different.
6. **Rider names + quotes** — `Kwabena A.` on `index.html` testimonial; `Kwabena Asante` and `Akosua Boateng` on `impact.html` (People + Path to Ownership + Financial Inclusion themes) — replace with consented quotes from real Wahu Heroes before publishing.
7. **Real photography for the eBike and eMoto hero stages on `vehicles.html`** — currently using lifestyle scene photos (`assets/ebike.jpg`, `assets/emoto-action.jpg`). Per the design brief, these should be studio shots on pure white. Lifestyle photos can stay on the impact page where they belong.
8. **Wire up Calendly** for the investors-page sequential CTA. The success state currently links to `https://calendly.com/wahu-investors` — confirm the real Calendly URL before launch.
9. **Add Plausible analytics** (or equivalent) snippet to all six pages — currently no analytics tag in any file.
10. **Mailto subject pre-fill encoding** — the eBike configurator order CTA links to `mailto:hello@wahu.me?subject=eBike%20order%20%E2%80%94%20%5Bcolour%2C%20battery%5D`. The bracketed placeholder `[colour, battery]` is intended to be hand-filled by the rider; once a real configurator with state is built, this should be wired to pass actual selections.
11. **Hero photos on `vehicles.html` model showcases** — when real studio shots replace the current photography, re-test that the spec-callout text is still readable against them (white text on white-ish backgrounds will need a stronger gradient overlay or repositioned text).

---

## Diff summary

- **Sections deleted:** 11 (`index`: 3 — duplicate vehicles video, offers cards, Hero stories video; `vehicles`: 1 — eMoto video; `business`: 3 — problems row, sidekick dark feature, keba dark feature, 90-sec tour video, who-it's-for grid; `impact`: 1 — A day with a Hero video; `investors`: 4 — stack table, pillars, flywheel, impact-inline; `careers`: 1 — workshop video). True total: index 3 + vehicles 1 + business 5 + impact 1 + investors 4 + careers 1 = **15**.
- **Sections rewritten (copy / CTAs / structure):** 27 across the six files (every hero, every final CTA, plus dashboard + form + commitments lede + thesis + ride-to-own framing, etc.).
- **Sections added:** 4 (eBike configurator, eMoto configurator, customer logo strip section, merged round+team).
- **Sections moved:** 2 (homepage how-it-works → vehicles ride-to-own; impact 2030 commitments moved to position 3).

---

## Suggested next pass (not in scope of this rewrite)

- **Mobile testing pass** — the new configurator block, the merged round+team layout, and the inline outcome strip on `business.html` were designed responsive but only quick-checked on a desktop viewport; do a real device pass.
- **Anchor link audit** — the new configurator blocks have IDs (`#ebike-configurator`, `#emoto-configurator`) referenced from the homepage tile CTAs and the vehicles final CTA. Verify the smooth-scroll lands cleanly when nav-fixed-header offset is taken into account; may need `scroll-margin-top: 96px` on the configurator sections.
- **Payment page** — the configurator currently terminates in a mailto. The next missing door, after this round of changes, is a real checkout/sign-up flow that captures the rider's KYC and the weekly payment mandate. That's the natural follow-on to the doc's "missing door on the entire site" framing.
- **Compare-page weekly-payment row** — the new `Weekly payment` row on the compare table reads `From GHS 280 / From GHS 380`. Once final pricing lands, consider showing the *total* paid-in over 18 months as well, so a rider can see the all-in commitment vs the bike's title value.
- **Demo form anti-spam** — the business demo form has no captcha. Consider Cloudflare Turnstile or hCaptcha before launch.
- **`index.html` reveal triggers** — the homepage final CTA section uses `.video-block` class but has no play button; consider renaming the class to `.cta-tile` (matching `vehicles.html` / `careers.html`) for clarity. Cosmetic — no behaviour change.
- **Investors page sequential CTA** — current behaviour shows the form inline and replaces it with a success state. Consider a small toast / scroll-into-view affordance so investors on tall screens don't miss the success state appearing below the fold.
