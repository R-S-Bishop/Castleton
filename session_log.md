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
