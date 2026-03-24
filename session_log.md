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
