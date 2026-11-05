# Coverly - Modern Wholesale Marketplace for Indian MSMEs

A production-grade MVP marketing site for **Coverly**, built with Next.js (App Router), TypeScript, Tailwind CSS, and Framer Motion. 

Theme: **"Warm Ledger"** - fintech-grade trust meets warm, human wholesale. Soft peach-to-cream canvas, crisp white surfaces, dark charcoal typography, deep navy primary actions, and a single coral accent used sparingly for action and lowest landed cost emphasis.

---

## 🚀 Quick Start

### 1. Install Dependencies
```bash
npm install
```

### 2. Run the Landed Cost Unit Tests
```bash
npm test
```
Runs 6 automated Vitest tests verifying:
- Tiruppur Knits (Rs212 unit + 5% GST + Rs3,200 freight / 500 = **Rs229.00**)
- Surat Textile Hub (Rs196 unit + 5% GST + Rs9,800 freight / 500 = **Rs225.40**)
- Ludhiana Garments Co (Rs205 unit + 5% GST + Rs2,400 freight / 500 = **Rs220.05**)
- Mathematical proof that the lowest sticker price (Surat: Rs196) is **not** the lowest landed cost (Ludhiana: Rs220.05)

### 3. Build & Run
```bash
npm run build
npm start
```
Open [http://localhost:3000](http://localhost:3000) to view the site.

---

## 🎨 Design Tokens & Theme ("Warm Ledger")

All tokens are defined as CSS variables in `app/globals.css` and mapped in `tailwind.config.ts`. No hardcoded hex values exist in components.

| Token | CSS Variable | Value | Purpose |
|---|---|---|---|
| Canvas Gradient Start | `--canvas-start` | `#F9DCD8` | Top page background gradient |
| Canvas Gradient End | `--canvas-end` | `#F5EAE6` | Bottom page background gradient |
| Surface Default | `--surface` | `#FFFFFF` | Primary card surfaces & tables |
| Surface Muted | `--surface-muted` | `#F6F7F9` | Hero container, secondary cards |
| Surface Pink | `--surface-pink` | `#FDECEB` | Metric cards & lowest cost rows |
| Text Primary | `--text-primary` | `#22252A` | High-contrast headings |
| Text Secondary | `--text-secondary` | `#7A7F87` | Body copy & subtle metadata |
| Primary Action | `--btn-primary` | `#1D2235` | Deep navy pill buttons |
| Accent Action | `--accent` | `#F16A5A` | Coral pill button & landed cost tag |
| Verified Badge | `--verified` | `#1F9D6B` | Verified supplier indicators |
| WhatsApp Green | `--whatsapp` | `#25D366` | Restricted to WhatsApp parser/chat button |

### Typography
- **Headings**: `Plus Jakarta Sans` (500-700 weight, tight tracking)
- **Body**: `Inter` (regular & medium, relaxed line-height)
- **Prices & Quantities**: `JetBrains Mono` with `tabular-nums`

---

## 📐 Page Structure & Section Breakdown

1. **Sticky Navigation (`components/sections/Navbar.tsx`)**
   - Coverly flame/stack mark logo in coral.
   - Smooth anchor navigation: *How it works*, *AI Parser*, *Live Demo*, *Trust*, *Contact*.
   - Right: "Log in" link + coral pill "Get Verified Quotes".
   - Responsive mobile drawer with keyboard focus control.

2. **Hero Section (`components/sections/Hero.tsx`)**
   - Split layout echoing the client's dual-screen composition.
   - Left container (`#F6F7F9`): Headline under 2 lines, subcopy strictly under 20 words, primary navy "Explore Live RFQ", secondary ghost button, and three stat cards (`48h response`, `120+ verified suppliers`, `True landed cost`).
   - Right stack: Soft-pink metric card (`#FDECEB`) with animated SVG line chart, plus a tilted dashboard card showing landed comparison.

3. **How It Works (`components/sections/HowItWorks.tsx`)**
   - 3-stage visual workflow: **Connect** -> **Compare** -> **Manage**.
   - Connected with a drawn dashed guide line.
   - Illustrative UI snippets in each card: RFQ match chip, landed cost formula badge, and order dispatch tracker.

4. **WhatsApp-to-Table Parser (`components/sections/AiParser.tsx`)**
   - Signature section highlighting Coverly's core technology moat.
   - Left: Realistic WhatsApp interface with messy supplier messages (Hinglish text, voice note chip with audio wave bars, paper rate-card attachment placeholder).
   - Right: Clean structured table with unit price, MOQ, freight, GST, and landed cost extraction. Includes a realtime re-parse scanning animation.

5. **Interactive Demo / RFQ Simulator (`components/sections/LiveDemo.tsx`)**
   - Category selector, custom quantity input, and destination city picker.
   - Pure typed calculation via `calculateLandedCost`:
     $$\text{landed\_per\_unit} = \frac{\text{unit\_price} \times \text{qty} \times (1 + \text{gst}) + \text{freight}}{\text{qty}}$$
   - Lowest landed cost row highlighted in coral with "Best landed cost" badge.
   - Automatic MOQ validation chip if order quantity is below supplier MOQ.
   - Dynamic dramatization banner showing net batch savings vs lowest sticker price.

6. **Trust & Verification Network (`components/sections/Trust.tsx`)**
   - "Backed by Rungta University Business Incubator, Bhilai" badge.
   - 4-step ground-truth audit: *Premise & GSTIN Audit*, *Capacity & MOQ Validation*, *Locked Freight Tariffs*, and *Quality Consistency*.
   - Trust-gap stat strip (sourced from `data/placeholders.ts`).
   - Partner ecosystem strip with text marks only (no fake corporate logos).

7. **Concierge Lead Form & Footer (`components/sections/Footer.tsx`)**
   - "Book a Sourcing Concierge" 48-hour pilot lead form with client-side validation.
   - Direct "Chat on WhatsApp" button.
   - Submission logs to console and transitions to a verified success screen.
   - Clearly marked `// TODO: Connect this form submission to real API endpoint` for backend integration.

---

## 📂 Where to Edit Copy & Data

- **All Placeholder Metrics**: `data/placeholders.ts`  
  Edit the hero stat numbers, trust gap percentages, and concierge turnaround times.
- **Supplier Demo Data & Categories**: `data/suppliers.ts` & `data/categories.ts`  
  Add or modify product categories, unit prices, freight rates, and GST percentages.
- **Section Copy**: Edit individual components in `components/sections/`.
- **Landed Cost Formula**: `lib/landed-cost.ts` and its test suite in `lib/landed-cost.test.ts`.

---

## 🏷️ List of Placeholders to Replace Before Production Launch

Per the project fact sheet (`docs/pitch-deck.md`), Coverly is an early-stage bootstrapped project with limited early validation. Every numeric claim below is currently a placeholder and must be verified before commercial deployment:

1. `PLACEHOLDERS.heroStats`:
   - `"48h Concierge response"` - Pilot service level target, not automated SLA.
   - `"120+ Verified suppliers"` - Target supply pipeline, not active inventory.
   - `"Avg savings: 12%"` - Indicative modeling; replace with actual customer basket data.
2. `PLACEHOLDERS.trustStats`:
   - `78%` of MSMEs sourcing via WhatsApp/phone (industry survey placeholder).
   - `8-12` quotes collected before single order (anecdotal discovery estimate).
   - `6-8 hrs/week` spent manually comparing quotes (anecdotal discovery estimate).
   - `15-40%` gap between quoted sticker and true landed cost (industry logistics estimate).
3. Partner & Logistics Network:
   - "Bhilai Industrial Zone", "Raipur Logistics Cluster", "Chhattisgarh MSME Network" are regional descriptive markers; replace with formally signed provider networks upon contract execution.
4. WhatsApp Contact Link:
   - Update `https://wa.me/919999999999` in `Footer.tsx` with Coverly's official WhatsApp Business number.
5. Concierge Lead Endpoint:
   - Connect `handleSubmit` in `Footer.tsx` to a CRM, webhook, or Supabase/Firebase backend.

---

## ⚖️ Facts vs. Sections Priority & Conflict Resolution

In accordance with project guidelines (*"Priority order: mockup-spec = visuals, pitch-deck = facts, sections.md = structure"*):
- **Incubation status**: Pitch deck confirms Coverly is associated with the **Rungta University Business Incubator, Bhilai** only (not DPIIT-registered or private limited). The site reflects this exact association.
- **Traction claims**: Pitch deck explicitly notes no revenue, user counts, or partner agreements have been finalized. All metrics are clearly marked with `/* PLACEHOLDER */` in `data/placeholders.ts`.
- **Logo wall**: The mockup showed sample logos (`freshworks`, `stripe`, etc.); per instructions, these were omitted and replaced with text-based regional ecosystem associations to avoid false representation.
- **Dash punctuation**: In compliance with the taste-skill directive (Section 9.G), zero em-dashes or en-dashes are used anywhere in the UI or codebase. Hyphens are used exclusively.
