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
| Colour palette — Style Guide v3.0 | Holly | Pending approval |
| GBT Airflow Hygiene fee — not on Fee Guide PDF; confirm whether separate fee or sits under Hygienist line | Holly | Pending |
| Referral inbox email address | Holly | Pending — blocks Formspree setup |
| Formspree account setup (free tier, formspree.io) | Holly → Ryan | Blocked — awaiting referral inbox email |
| DentalHub — supply new Castleton logo once finalised | Holly → Ryan | Pending — awaiting final logo |
| Privacy Policy HTML page | Ryan | Pending |
| Embedded Google Maps — home page | Ryan | Pending |
| Google Maps Place ID — retrieve from Maps embed (no login needed) and pass to Ryan to pin exactly to GBP listing | Holly / Ryan | ✅ Complete — Place ID: `0x48742daba0c2eb6d:0x4a77be4480f6da66` |
| Google Business Profile — upload new building & team photography once available (mirrors website assets, boosts local SEO) | Holly | Pending — awaiting photography |
| Google Maps custom logo pin — requires Maps JavaScript API key (see guide below) | Holly → Ryan | Pending |

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

*Note: `styles.css` is at v3.0 per approved Style Guide v3.0 — March 2026.*
