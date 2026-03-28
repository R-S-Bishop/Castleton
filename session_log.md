# Session Log — Castleton Dental Website Build

---

## Session 5 — 28 March 2026

**Attendees:** Ryan Bishop (ryanbishop.co.uk)

### Context
Claude Code session. Focus on nav logo replacement, logo interactivity, building photography in hero, and hero layout/typography improvements.

### Work Completed

#### 1. Nav logo — replaced with house illustration across all pages
`castleton-logo.png` replaced with `castleton-house.png` (the new transparent illustrated house logo) in both the desktop left sidebar and the mobile top bar, across all 21 HTML pages (13 root-level + 8 `/treatments/` subpages).

**Files changed:** All HTML pages in `/` and `/treatments/`

#### 2. Logo made clickable — returns to home page
Both logo instances (desktop sidebar + mobile top bar) wrapped in `<a>` links. Root-level pages link to `index.html`; treatments subpages link to `../index.html`. No JavaScript required — plain anchor tag.

**Files changed:** All HTML pages in `/` and `/treatments/`

#### 3. `nav-left__wordmark` removed — sidebar text below logo
The "castleton / Dental Practice" `<p>` element below the logo in the left sidebar was removed. The equivalent wordmark in the top bar (`nav-top__wordmark`) was retained — this is the text to the right of the logo visible on desktop.

**Files changed:** All HTML pages in `/` and `/treatments/`

#### 4. Building photography added to hero — `index.html`
`<!-- TBC: building photography -->` placeholder replaced with the actual building photograph. CSS updated simultaneously: placeholder background and flex-centering removed; brass border (`3px solid var(--color-brass)`) and `overflow: hidden` added.

**Note:** Initial src pointed to `castleton-house.jpg` (the old illustrated logo); corrected to `castleton_outside.jpeg` after the building photograph was uploaded to `images/` by client.

**Files changed:** `index.html`, `styles.css`

#### 5. Hero image spacing
Added `margin-top: var(--space-10)` (40px) to `.hero__image` to give breathing room between the "Refer a Patient" CTA and the photograph below it.

**Files changed:** `styles.css`

#### 6. Hero typography — fluid scaling with `clamp()`
Hero text was fixed-size and became cramped at narrower viewport widths (e.g. half-screen iMac). All three hero text elements converted to fluid `clamp()` values:

| Element | Before | After |
|---|---|---|
| `.hero__title` | `3.25rem` (fixed) | `clamp(1.75rem, 2.5vw + 0.5rem, 3.25rem)` |
| `.hero__subtitle` | `1.125rem` (fixed) | `clamp(1rem, 1vw + 0.5rem, 1.125rem)` |
| `.hero__body` | `1rem` (fixed) | `clamp(0.9rem, 0.5vw + 0.75rem, 1rem)` |

Title now scales from 28px (small viewports) to 52px (full width) rather than sitting on 3 lines at intermediate sizes.

**Files changed:** `styles.css`

#### 7. Hero image — border sizing and alignment fixes
Two layout bugs resolved:

- **Border oversized:** `min-height: 400px` was forcing the brass border taller than the photograph, leaving an empty gap. Removed `min-height`; changed `height: 100%` → `height: auto` on `.hero__image img` so the border hugs the photo at any width.
- **Image left-aligned:** Added `margin-inline: auto` to `.hero__image` for centred alignment on single-column (mobile/narrow) viewports.
- **Two-column grid not working:** The 768px breakpoint grid (`1fr 1fr`) was applied to `.hero` (the `<section>`), whose only direct child is `.container` — so the grid had no effect. Moved to `.hero .container` so `hero__content` and `hero__image` become proper grid items. Margin overrides reset within the 768px breakpoint so the image fills its column naturally.

**Files changed:** `styles.css`

#### 8. Favicon discussion
Discussed whether `castleton-house.png` (illustrated house, transparent background) would work as a favicon. Conclusion: likely workable — the illustration is already rendering cleanly in the browser tab at small sizes (visible in staging screenshots), and the transparent background is an advantage. Landscape aspect ratio may require a square crop. The existing `<!-- TBC: replace with Castleton favicons -->` comment remains in all `<head>` blocks pending logo finalisation.

**No files changed.**

---

## Session 1 — 24 March 2026

**Attendees:** Ryan Bishop (ryanbishop.co.uk)

### Context
First Claude Code session on the Castleton Dental website build. Working from the skeleton HTML committed to GitHub and the CAS001_Website build folder on Desktop.

### Files Reviewed
- All HTML pages in `/` and `/treatments/` (GitHub repo)
- `styles.css`
- `Phase 5 - Content & Brand/Castleton Content Mapping.docx` — full content status map
- `Phase 3 - Digital Asset Audit/Fee Guide 2026.pdf` — official fee schedule Jan 2026
- `Phase 2 - Scoping Call/Castleton_Meeting_Minutes.docx` — agreed brief and decisions
- `Phase 2 - Scoping Call/logos and leaflets for new patients/` — logo and building assets

### Work Completed

#### 1. `prices.html` — Full fee guide populated
Replaced all `TBC` placeholder content with real fees from the official **Fee Guide Jan 2026** PDF.

Sections added:
- **General & Preventative** — examinations (new patient, regular, children by age band), emergency, radiograph, hygienist, missed appointment policy
- **Restorative** — amalgam and composite fillings, root canal (incisor/premolar/molar), acrylic and metal dentures
- **Cosmetic Dentistry** — cosmetic fillings, tooth whitening, crowns, veneers, Invisalign (single and double arch)
- **Implants & Oral Surgery** — implant placement, PRF, implant crown
- **Other** — sports mouthguards (coloured and patterned)

All sections now include a **CDM Member** column showing included items and 10% discounts where applicable.

Footnote added: *"All fees are intended as a guide only. A written treatment estimate will be provided prior to commencing treatment. Fees correct as of January 2026."*

CDM membership section updated with descriptive copy and dual CTA (Ask About Membership / Book an Appointment).

#### 2. Digital assets copied to repo
Created `images/` directory and copied the following as placeholders (logo in development):
- `images/castleton-logo.png`
- `images/castleton-logo.jpg`
- `images/castleton-house.jpg`

---

## Session 2 — 24 March 2026

**Attendees:** Ryan Bishop (ryanbishop.co.uk)

### Context
Follow-on session. Holly reviewing the staging site shared after Session 1. Focus on improving the contact page map embed.

### Work Completed

#### 1. `contact.html` — Google Maps iframe with correct pin

**Problem:** The original `<iframe>` embed used a placeholder URL with no valid place ID (`!1s0x0%3A0x0`), so no pin was ever rendered on load.

**Approach discussed:** Initially implemented Leaflet.js + OpenStreetMap with a custom logo marker. After review, reverted to a standard Google Maps iframe — simpler, no third-party dependencies, and more familiar/trusted by users.

**Solution:** Google Maps iframe using a business name + address query URL. Google resolves this to its own verified listing and drops the standard red pin automatically. No API key required.

```
https://maps.google.com/maps?q=Castleton+Dental+Practice,+11+Castle+Street,+Farnham,+GU9+7JA&z=16&output=embed
```

**Note on custom logo pin:** Replacing Google's red pin with a branded logo marker requires the Google Maps JavaScript API (free tier, but needs a billing-enabled Google Cloud account). Deferred — can revisit if Holly requests it.

**Files changed:**
- `contact.html`
- `styles.css`

**Commit:** `Revert to Google Maps iframe — remove Leaflet/OpenStreetMap implementation`

> ⚠️ **Push required** — commits are staged locally. Push via GitHub Desktop or terminal (`git push origin main`) as SSH/token auth was not available in this session.

---

## Session 3 — 25 March 2026

**Attendees:** Ryan Bishop (ryanbishop.co.uk)

### Context
Planning session via Claude (claude.ai). Focus on colour palette refinement following Holly's feedback on the staging site, referral form upgrade, and style guide versioning. No Claude Code used — all changes prepared for manual push via GitHub Desktop.

### Work Completed

#### 1. `styles.css` — Palette updated to v3.0

Two palette iterations in this session, both driven by Holly's feedback:

**v2.0 → changes from Holly's palette image:**
Mint-based palette replaced entirely with warm olive and linen tones. Holly specifically flagged mint as "too NHS" in character.

| Variable | v1.0 | v2.0 |
|---|---|---|
| `--color-primary` | `#7ccba6` Arsenic | `#8A8E75` Olive |
| `--color-primary-dark` | `#31694c` Deep Forest | `#68604D` Dark Olive |
| `--color-primary-mid` | `#77b197` Sage | `#BEC5A4` Sage Soft |
| `--color-primary-light` | `#a3d2bd` Soft Mint | `#D5C7AD` Sand |
| `--color-bg` | `#ebfaf4` Off-White Mint | `#F1EAD8` Linen |
| `--color-brass` | `#B5935A` | `#B5935A` ✓ Confirmed |

**v3.0 → Sage Soft and Dark Olive swapped in hierarchy:**
Sage Soft (`#BEC5A4`) now governs navigation, CTAs, and active states. Dark Olive (`#68604D`) moves to secondary actions and hover states. Olive (`#8A8E75`) unchanged as primary brand colour.

| Variable | v2.0 | v3.0 |
|---|---|---|
| `--color-primary-dark` | `#68604D` Dark Olive | `#BEC5A4` Sage Soft |
| `--color-primary-mid` | `#BEC5A4` Sage Soft | `#68604D` Dark Olive |

**Files changed:**
- `styles.css`

#### 2. `referrals.html` — Full referral form rebuild

Rebuilt to match the structure of toothbeary.co.uk/referrals (provided as reference by Holly). Previous form replaced entirely.

**Three-section layout:**
- **Section 1 — Referring Practice:** Practice name, dentist name, email, phone, address
- **Section 2 — Patient Details:** Name, DOB, phone, email, treatment type dropdown (all six confirmed referral categories), clinical notes, urgency selector
- **Section 3 — Supporting Files:** Drag-and-drop file upload zone, accepts PDF/JPG/PNG up to 5MB, file list display

**Additional features:**
- Privacy consent checkbox with brass left border accent — required before submission
- Honeypot spam prevention field
- Brass-numbered section strip headers
- Dark Olive sidebar listing accepted referral types with contact fallback
- Async submission via Formspree — form hides on success, confirmation message shown
- Graceful error handling with phone/email fallback

**Important — Formspree dependency:**
File uploads cannot be handled by GitHub Pages (static host only). Formspree provides the server layer. Dependency chain:

> Holly confirms referral inbox email → Holly creates Formspree account (formspree.io, free tier) → Holly sends 8-character form ID to Ryan → Ryan replaces `TBC-FORMSPREE-ID` in `referrals.html` → Done

**Files changed:**
- `referrals.html`

#### 3. `styles.css` — Social icon hover states confirmed
Inline SVG icons (Instagram, Facebook, LinkedIn) in footer. Instagram links to confirmed `castletondental` account. Facebook and LinkedIn remain `href="#"` pending Holly confirmation.

#### 4. Style Guide — v2.0 and v3.0 produced
- **Castleton_Style_Guide_v2.docx** — warm olive/linen palette, visual preview page, change tracking table v1→v2, approval table
- **Castleton_Style_Guide_v3.docx** — Sage Soft ↔ Dark Olive swap, change tracking table v2→v3, header/footer matched exactly to v2 reference file

Both sent to Holly for approval.

---

## Session 4 — 26 March 2026

**Attendees:** Ryan Bishop (ryanbishop.co.uk)

### Context
Planning and design session via Claude (claude.ai). Focus on L-shaped sticky nav — concept design, iterative refinement via browser screenshots, Style Guide v3 update, and full implementation across all 16 pages. No Claude Code used — all changes packaged in skeleton v7 for manual push via GitHub Desktop.

### Work Completed

#### 1. Nav concept — L-shaped sticky nav designed and iterated

Castleton Dental requested a nav forming an L-shape: a fixed vertical column on the left and a fixed horizontal bar across the top, meeting at a smooth concave arc (described as "a road turn, not a T-junction"). Multiple iterations produced and reviewed via browser screenshots.

**Final spec:**

| Element | Detail |
|---|---|
| Left column | 200px fixed width, full viewport height, Sage Soft background |
| Top bar | Full width minus left column, 60px height, Sage Soft background |
| Arc junction | 56px radius, radial-gradient technique — Sage Soft regardless of page content scrolling behind |
| Logo | `images/castleton-logo.png` in left column, 140px wide |
| Left column content | Logo, brass divider, contact details (phone, email, address, hours), Book an Appointment (primary CTA), Refer a Patient (secondary CTA), TBC slot for future CTAs |
| Top bar content | Wordmark ("castleton / DENTAL PRACTICE" — text only, no duplicate logo), brass divider, nav links |
| Nav link states | Rest: Ink on Sage Soft / Hover + active: White on Dark Olive pill |
| Mobile | Left column hidden, top bar full width, logo in top bar, hamburger → drawer with links and CTAs |

**Arc technique:** A `div.nav-arc` with `radial-gradient(circle at 100% 100%, transparent [radius], Sage Soft [radius])` creates a concave curve that remains Sage Soft regardless of page section colour scrolling behind. Earlier approach (page-background coloured div with `border-radius`) was abandoned as it exposed incorrect colour when scrolling over white sections.

**Iterations:**
- v1: Initial concept — arc too small (40px), logo constrained to top bar height
- v2: Arc increased to 56px, logo freed with generous padding, wordmark added to top bar alongside small logo
- v3: Small logo removed from top bar (wordmark text only), arc overlap offset removed (caused visible protrusion), CTAs repositioned below contact details
- v4 (final): Arc gradient tightened, proportions confirmed, all three feedback points resolved

**Concept file:** `castleton_nav_concept.html` (standalone, self-contained, for sharing or archiving)

#### 2. Style Guide v3.0 — Key Components section updated and finalised

Before sending to Holly, Section 6 (Key Components) updated to reflect the agreed nav:

- **Navigation** — replaced generic bullet list with a structured table: left column, top bar, arc, mobile
- **Navigation link states** — new table documenting Ink at rest / Dark Olive hover, confirmed in concept
- **Left column CTAs** — own table: Book an Appointment (primary), Refer a Patient (secondary), extensible TBC slot
- **Buttons (page content)** — updated to v3 palette; old v1 hex values removed; Brass accent added as third type for PDF downloads
- **Cards** — Sand border (#D5C7AD) replacing old mint reference
- **Photography** — "client" replaced with "Castleton Dental" and "Holly" per house style
- **Approval table** — navigation split into two rows (layout pending / link states confirmed)

**Style Guide v3.0 sent to Holly.**

#### 3. L-shaped nav implemented across all 16 pages — skeleton v7

Script-based approach replaced the old single-bar nav simultaneously across all pages. Zero changes to any page content.

**What changed on every page:**
- Old contact bar and single-bar nav block removed
- L-shaped nav inserted: `nav-left`, `nav-arc`, `nav-top`, mobile drawer
- `<main>` gains `class="page-main"` providing `margin-left: var(--left-width)` on desktop
- Hamburger JS updated to target new element IDs

**What did not change:**
- All `<head>` content — GTM, Cookiebot, GA4, meta tags, canonical, structured data, noindex
- Every section, heading, paragraph, form, and footer
- All CSS design tokens and custom properties

**Treatment subpages** — logo and all internal links correctly use `../` prefix. Verified.

**`styles.css` changes:**
- Old nav CSS block fully replaced (`.nav`, `.nav__inner`, `.nav__logo`, `.nav__contact-bar` etc.)
- New L-shaped nav CSS added: left column, top bar, arc, page-main offset, mobile breakpoint
- `--left-width: 200px`, `--top-height: 60px`, `--arc-radius: 56px` in `:root` — single-value iteration for proportional changes
- Obsolete tablet breakpoint nav overrides removed

**Files changed:**
- All 16 HTML pages (`/` and `/treatments/`)
- `styles.css`

**Deliverable:** `castleton_skeleton_v7.zip`

---

### Outstanding / TBC Items

| Item | Owner | Status |
|---|---|---|
| Team bios and photos | Holly | Pending |
| About page copy (new ownership narrative) | Holly / copywriting | Pending |
| Hero copy tone edit | Copywriting | Pending |
| Building photography (hero image) | Holly | Pending |
| Cookiebot account ID | Holly | Pending |
| Google Tag Manager container ID | Holly | Pending |
| GA4 measurement ID | Holly | Pending |
| Facebook account URL | Holly | Pending |
| LinkedIn account URL | Holly | Pending |
| Final logo files (SVG/EPS) | Holly | In development |
| Colour palette & nav layout — Style Guide v3.0 | Holly | Sent — pending approval |
| GBT Airflow Hygiene fee — confirm whether separate fee or under Hygienist line | Holly | Pending |
| Referral inbox email address | Holly | Pending — blocks Formspree setup |
| Formspree account setup (free tier, formspree.io) | Holly → Ryan | Blocked — awaiting referral inbox email |
| DentalHub — supply new Castleton logo once finalised | Holly → Ryan | Pending — awaiting final logo |
| Privacy Policy HTML page | Ryan | Pending |
| Embedded Google Maps — home page | Ryan | Pending |
| Google Maps Place ID | Holly / Ryan | ✅ Complete — Place ID: `0x48742daba0c2eb6d:0x4a77be4480f6da66` |
| Google Business Profile — upload photography once available | Holly | Pending — awaiting photography |
| Google Maps custom logo pin — requires Maps JavaScript API key (see Appendix) | Holly → Ryan | Pending |

---

## Appendix — Google Maps Custom Logo Pin: Step-by-Step Guide for Holly

The map on the Contact page currently shows Google's standard red pin. To replace it with the Castleton logo, a **Google Maps JavaScript API key** is needed. This is free for a site of this size — Google provides $200/month credit, and a dental practice website will use a tiny fraction of that.

### What Holly needs to do

**Step 1 — Create a Google Cloud project**
1. Go to [console.cloud.google.com](https://console.cloud.google.com) and sign in with the practice's Google account (the same one used for Google Business Profile)
2. Click **Select a project** (top left) → **New Project**
3. Name it `Castleton Dental Website` → **Create**

**Step 2 — Enable the Maps JavaScript API**
1. In the left menu go to **APIs & Services → Library**
2. Search for `Maps JavaScript API` → click it → **Enable**

**Step 3 — Set up billing**
1. Go to **Billing** in the left menu
2. Link a credit/debit card — required by Google but the $200/month free credit means no charge for normal website traffic
3. Google will not charge unless usage far exceeds the free tier (extremely unlikely for a dental practice)

**Step 4 — Create an API key**
1. Go to **APIs & Services → Credentials**
2. Click **Create Credentials → API Key**
3. Copy the key — it will look like: `AIzaSyXXXXXXXXXXXXXXXXXXXXXXXXXXXXX`

**Step 5 — Restrict the key (important for security)**
1. Click on the key to edit it
2. Under **Application restrictions** select **Websites**
3. Add both: `https://www.castletondental.co.uk/*` and `https://castletondental.co.uk/*`
4. Under **API restrictions** select **Restrict key** → choose `Maps JavaScript API`
5. Click **Save**

**Step 6 — Pass the key to Ryan**
Send the API key securely — Ryan will implement the branded logo pin on the Contact page.

> **Never share the API key publicly or commit it to GitHub.** The domain restriction in Step 5 ensures it can only be used on the Castleton website.

---

*Note: `styles.css` at v3.0 per Style Guide v3.0 — March 2026. Skeleton at v7.*

---

## Session 4 — 27 March 2026

**Attendees:** Ryan Bishop (ryanbishop.co.uk)

### Work Completed

| Task | Notes |
|---|---|
| Restored GBP Google Maps embed | Both `contact.html` and `index.html` — Place ID `0x48742daba0c2eb6d:0x4a77be4480f6da66` had been overwritten by the new arc nav commit; now fixed on both pages |
| Mobile navigation — full diagnosis and fix | See detail below |

### Mobile Navigation — Diagnosis & Fixes

**Root cause of unresponsive hamburger on iPhone:**
Every page contained two conflicting `<script>` blocks — an old `nav--open` script (pre-arc nav) and the new arc nav script — both declaring `const hamburger`. Browsers throw a `SyntaxError` on duplicate `const` declarations, silently killing all nav JS on the page.

**All fixes applied (23 files changed):**

1. **Stale JS removed** — Old `nav--open` script blocks purged from all 20 active HTML pages
2. **Backdrop overlay** — `.nav-overlay` div created dynamically in JS; dims content behind open drawer; tapping overlay closes the drawer
3. **Hamburger → × animation** — CSS transitions on the three spans; animates to × when `menu-open` is on `body`
4. **Border selector bug fixed** — `.nav-mobile-drawer a:last-child` changed to `> a:last-of-type` so the Contact nav link correctly loses its bottom border

