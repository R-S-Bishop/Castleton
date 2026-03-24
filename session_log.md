# Session Log — Castleton Dental Website Build

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

#### 1. `contact.html` — Interactive Leaflet.js map replacing broken Google Maps iframe

**Problem:** The previous `<iframe>` embed used a placeholder Maps URL with no valid place ID (`!1s0x0%3A0x0`), so no pin was ever rendered on load.

**Solution:** Replaced the iframe entirely with a [Leaflet.js](https://leafletjs.com/) interactive map backed by OpenStreetMap tiles. No Google Maps API key required.

**Custom branded marker:**
- Castleton logo (`images/castleton-logo.png`) displayed inside a white speech-bubble pin with a **deep forest green** (`#31694c`) border and downward-pointing spike
- Pin anchored precisely to coordinates `51.21435, -0.79858` (11 Castle Street, Farnham)
- Popup opens by default showing address and click-to-call `01252 715576`
- Scroll-wheel zoom disabled (prevents accidental scroll-hijack on the contact page)

**CSS added to `styles.css`:**
- `#castleton-map` — sets the Leaflet canvas to 320px height
- `.cdp-pin`, `.cdp-pin__bubble`, `.cdp-pin__spike` — custom marker component
- `.leaflet-popup-content-wrapper` — Leaflet popup styled to match brand typography

**Files changed:**
- `contact.html`
- `styles.css`

**Commit:** `Replace static map iframe with Leaflet.js interactive map with branded logo pin`

> ⚠️ **Push required** — commit is staged locally. Push via GitHub Desktop or terminal (`git push origin main`) as SSH/token auth was not available in this session.

---

### Outstanding / TBC Items (from Content Mapping)
The following remain open for future sessions:

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
| Colour palette confirmation | Holly | Pending |
| GBT Airflow Hygiene fee — not on Fee Guide PDF; confirm whether separate fee or sits under Hygienist line | Holly | Pending |
| Referral form build | Ryan | Pending |
| Privacy Policy HTML page | Ryan | Pending |
| Embedded Google Maps (contact + home) | Ryan | contact.html ✅ — home TBC |

---
