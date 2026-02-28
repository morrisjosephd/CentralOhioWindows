# Central Ohio Windows Lead-Gen Website Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Build a 20+ page lead-generation website at centralohiowindows.com that captures homeowner info for window replacement and sells exclusive leads to window contractors.

**Architecture:** Static Astro v5 site with reusable components, Netlify Forms for lead capture, and dynamic routes for 14 city landing pages. All content pages link back to a central `/free-quote` form. Design uses Tailwind CSS v4 + daisyUI v5 with a professional blue/white theme.

**Tech Stack:** Astro v5, Tailwind CSS v4, daisyUI v5, astro-seo, @astrojs/sitemap, Netlify Forms

**Design Doc:** `docs/plans/2026-02-27-lead-gen-website-design.md`

---

## Task 1: Configure Theme and Global Styles

**Files:**
- Modify: `src/styles/global.css`

**Step 1: Update global.css with daisyUI theme configuration**

```css
@import "tailwindcss";
@plugin "daisyui" {
  themes: light --default;
}

@theme {
  --color-brand-blue: #1e40af;
  --color-brand-blue-light: #3b82f6;
  --color-brand-blue-dark: #1e3a8a;
}
```

This uses daisyUI's built-in `light` theme as default and adds custom brand colors via Tailwind v4's `@theme` directive.

**Step 2: Verify build**

Run: `npm run build`
Expected: Build succeeds with no errors

**Step 3: Commit**

```bash
git add src/styles/global.css
git commit -m "feat: configure daisyUI light theme and brand colors"
```

---

## Task 2: Build Header Component

> Use @frontend-design skill for visual quality

**Files:**
- Create: `src/components/Header.astro`
- Modify: `src/layouts/BaseLayout.astro`

**Step 1: Create the Header component**

Build a responsive navbar using daisyUI's `navbar` component with:
- Logo text "Central Ohio Windows" in `navbar-start`
- Navigation links in `navbar-center` (hidden on mobile, visible on lg+): Home, Window Types, Cost Guide, About
- Mobile hamburger dropdown menu using daisyUI `dropdown` for small screens
- "Get Free Quote" primary button in `navbar-end`
- All links use `<a>` tags with correct paths

daisyUI classes to use: `navbar`, `navbar-start`, `navbar-center`, `navbar-end`, `btn`, `btn-primary`, `dropdown`, `menu`

**Step 2: Add Header to BaseLayout**

In `src/layouts/BaseLayout.astro`, import and render `<Header />` above `<slot />` in the body.

**Step 3: Verify build**

Run: `npm run build`
Expected: Build succeeds

**Step 4: Commit**

```bash
git add src/components/Header.astro src/layouts/BaseLayout.astro
git commit -m "feat: add responsive Header component with navigation"
```

---

## Task 3: Build Footer Component

> Use @frontend-design skill for visual quality

**Files:**
- Create: `src/components/Footer.astro`
- Modify: `src/layouts/BaseLayout.astro`

**Step 1: Create the Footer component**

Build a site footer using daisyUI's `footer` component with:
- Three nav columns: "Resources" (Cost Guide, Window Types, Energy Efficient, Signs You Need New Windows), "Service Areas" (Columbus, Dublin, Westerville, + "All Areas" link), "Company" (About, Free Quote, Privacy Policy)
- Bottom bar with copyright: "© 2025 Central Ohio Windows. All rights reserved."
- Disclaimer text: "Central Ohio Windows is a free resource that connects homeowners with local window contractors."
- Background: `bg-neutral text-neutral-content`

daisyUI classes: `footer`, `sm:footer-horizontal`, `footer-title`, `link link-hover`

**Step 2: Add Footer to BaseLayout**

In `src/layouts/BaseLayout.astro`, import and render `<Footer />` below `<slot />` in the body.

**Step 3: Verify build**

Run: `npm run build`
Expected: Build succeeds

**Step 4: Commit**

```bash
git add src/components/Footer.astro src/layouts/BaseLayout.astro
git commit -m "feat: add Footer component with links and disclaimer"
```

---

## Task 4: Build LeadCaptureForm Component

**Files:**
- Create: `src/components/LeadCaptureForm.astro`

**Step 1: Create the form component**

Build the 6-field lead capture form with Netlify Forms integration:

```html
<form name="lead-capture" method="POST" data-netlify="true" netlify-honeypot="bot-field">
  <input type="hidden" name="form-name" value="lead-capture" />
  <p class="hidden"><label>Don't fill this out: <input name="bot-field" /></label></p>
  <!-- 6 visible fields -->
</form>
```

Fields use daisyUI's `fieldset`, `label`, `input`, `select` classes:
1. Full Name — `<input type="text" name="name" class="input" required>`
2. Phone Number — `<input type="tel" name="phone" class="input" required>`
3. Email — `<input type="email" name="email" class="input" required>`
4. Address or ZIP — `<input type="text" name="address" class="input" required>`
5. Number of Windows — `<select name="window-count" class="select">` with options: "1-3", "4-7", "8-12", "13+"
6. Project Timeline — `<select name="timeline" class="select">` with options: "ASAP", "Within 1 month", "1-3 months", "Just researching"

CTA button: `<button type="submit" class="btn btn-primary btn-lg w-full">Get My Free Quote</button>`

Below form: trust text "Your information is safe. We only share it with one vetted local contractor."

The component should accept an optional `heading` prop (string) to allow different headings when embedded on different pages.

**Step 2: Verify build**

Run: `npm run build`
Expected: Build succeeds

**Step 3: Commit**

```bash
git add src/components/LeadCaptureForm.astro
git commit -m "feat: add LeadCaptureForm component with Netlify Forms"
```

---

## Task 5: Build CTABlock Component

**Files:**
- Create: `src/components/CTABlock.astro`

**Step 1: Create the CTA block component**

A reusable inline call-to-action block used on content pages. Props:
- `heading` (string, default: "Ready for Your Free Estimate?")
- `description` (string, default: "Get matched with a trusted local window contractor. No pressure, no spam.")
- `buttonText` (string, default: "Get My Free Quote")
- `buttonHref` (string, default: "/free-quote")

Structure: centered section with background color (`bg-brand-blue` or `bg-primary`), white text, heading, description, and a prominent button linking to the quote page.

**Step 2: Verify build**

Run: `npm run build`
Expected: Build succeeds

**Step 3: Commit**

```bash
git add src/components/CTABlock.astro
git commit -m "feat: add CTABlock component for inline calls-to-action"
```

---

## Task 6: Build HowItWorks Component

**Files:**
- Create: `src/components/HowItWorks.astro`

**Step 1: Create the component**

A 3-step visual process section:
1. "Tell Us About Your Project" — with a clipboard/form icon (use SVG or emoji as placeholder)
2. "We Match You with the Right Pro" — with a handshake/matching icon
3. "Get Your Free, No-Pressure Quote" — with a checkmark/quote icon

Layout: 3-column grid on desktop (`grid grid-cols-1 md:grid-cols-3 gap-8`), stacking on mobile. Each step has a number badge, icon area, title, and short description.

**Step 2: Verify build**

Run: `npm run build`
Expected: Build succeeds

**Step 3: Commit**

```bash
git add src/components/HowItWorks.astro
git commit -m "feat: add HowItWorks 3-step process component"
```

---

## Task 7: Build FAQ Component

**Files:**
- Create: `src/components/FAQ.astro`

**Step 1: Create the component**

An accordion FAQ using daisyUI's collapse + join pattern. Props:
- `items` — array of `{ question: string, answer: string }`

```html
<div class="join join-vertical w-full">
  {items.map((item, i) => (
    <div class="collapse collapse-arrow join-item border border-base-300">
      <input type="radio" name="faq-accordion" checked={i === 0} />
      <div class="collapse-title font-semibold">{item.question}</div>
      <div class="collapse-content text-sm">{item.answer}</div>
    </div>
  ))}
</div>
```

**Step 2: Verify build**

Run: `npm run build`
Expected: Build succeeds

**Step 3: Commit**

```bash
git add src/components/FAQ.astro
git commit -m "feat: add FAQ accordion component"
```

---

## Task 8: Build Homepage

> Use @frontend-design skill for visual quality

**Files:**
- Modify: `src/pages/index.astro`

**Step 1: Build the full homepage**

Replace the placeholder content with the complete homepage using these sections in order:

1. **Hero Section** — daisyUI `hero` component with gradient background
   - H1: "Find a Trusted Window Replacement Pro in Central Ohio"
   - Subtitle: "Get a free, no-obligation quote from one vetted local contractor. No pressure, no spam."
   - CTA button: "Get My Free Quote" → `/free-quote`
   - Trust badge row: three badges ("Free Estimates", "No Obligation", "One Trusted Contractor")

2. **HowItWorks** — import and render the component

3. **Why Homeowners Trust Us** — 3-card grid using daisyUI cards
   - "One Contractor, Not Five" — Unlike other sites, we connect you with just one trusted pro
   - "Your Info Stays Private" — We never share without your permission
   - "100% Free for Homeowners" — Contractors pay us, not you

4. **Service Areas** — Grid of 14 city cards, each linking to its city page
   - Use daisyUI cards or a simple grid of linked items
   - Cities: Columbus, Westerville, Dublin, Hilliard, Grove City, Worthington, Powell, Pickerington, Reynoldsburg, Delaware, Newark, Lancaster, Springfield, Mansfield

5. **Popular Resources** — 3-4 cards linking to content pages (Cost Guide, Window Types, Signs You Need New Windows, Energy Efficient Windows)

6. **CTABlock** — import and render with default props

7. **FAQ** — import and render with homepage FAQs:
   - "How does Central Ohio Windows work?"
   - "Is this really free?"
   - "How many contractors will contact me?"
   - "What areas do you serve?"
   - "How do you choose which contractor to match me with?"

Update SEO metadata:
- Title: "Central Ohio Windows | Find Trusted Window Replacement Pros"
- Description: "Get a free, no-obligation quote from a vetted local window contractor in Central Ohio. One contractor. One quote. Zero pressure."

**Step 2: Verify build**

Run: `npm run build`
Expected: Build succeeds

**Step 3: Commit**

```bash
git add src/pages/index.astro
git commit -m "feat: build complete homepage with hero, how-it-works, and service areas"
```

---

## Task 9: Build Free Quote Page

**Files:**
- Create: `src/pages/free-quote.astro`

**Step 1: Create the free quote page**

A conversion-focused page with:
1. Heading: "Get Your Free Window Replacement Quote"
2. Subheading: "Tell us about your project and we'll match you with a trusted local contractor."
3. The `LeadCaptureForm` component
4. Trust signals sidebar or below-form section:
   - "No spam — ever"
   - "One contractor, not five"
   - "Your info stays private"
   - "Free, no-obligation quote"

SEO metadata:
- Title: "Get a Free Window Replacement Quote | Central Ohio Windows"
- Description: "Request your free, no-obligation window replacement quote. We'll match you with one trusted local contractor in Central Ohio. No pressure, no spam."

**Step 2: Create the form success page**

Create `src/pages/thank-you.astro`:
- Heading: "Thank You!"
- Message: "We've received your information. A trusted local window contractor will be in touch within 24 hours."
- Link back to homepage

Configure the form's `action` attribute to point to `/thank-you`.

SEO metadata:
- Title: "Thank You | Central Ohio Windows"
- Description: "Your free quote request has been received."

**Step 3: Verify build**

Run: `npm run build`
Expected: Build succeeds

**Step 4: Commit**

```bash
git add src/pages/free-quote.astro src/pages/thank-you.astro
git commit -m "feat: add free quote page with lead capture form and thank-you page"
```

---

## Task 10: Build City Landing Pages with Dynamic Routes

**Files:**
- Create: `src/data/cities.ts`
- Create: `src/pages/[city]-ohio-windows.astro`

**Step 1: Create city data file**

Create `src/data/cities.ts` with an array of city objects:

```typescript
export interface City {
  slug: string;
  name: string;
  description: string;
  highlights: string[];
  faq: { question: string; answer: string }[];
}

export const cities: City[] = [
  {
    slug: "columbus",
    name: "Columbus",
    description: "As Ohio's capital and largest city, Columbus has a diverse housing stock...",
    highlights: ["German Village historic homes", "Clintonville bungalows", "Dublin new construction"],
    faq: [
      { question: "How much do replacement windows cost in Columbus?", answer: "..." },
      { question: "What window styles are popular in Columbus?", answer: "..." },
    ]
  },
  // ... 13 more cities: Westerville, Dublin, Hilliard, Grove City, Worthington,
  //     Powell, Pickerington, Reynoldsburg, Delaware, Newark, Lancaster,
  //     Springfield, Mansfield
];
```

Each city should have unique description text mentioning local neighborhoods, housing characteristics, and common window issues. The FAQ answers should reference local details.

**Step 2: Create the dynamic route page**

Create `src/pages/[city]-ohio-windows.astro` using Astro's `getStaticPaths()`:

```astro
---
import { cities } from '../data/cities';
// ... other imports

export function getStaticPaths() {
  return cities.map(city => ({
    params: { city: city.slug },
    props: { city },
  }));
}

const { city } = Astro.props;
---
```

Page structure for each city:
1. H1: "Window Replacement in [City], Ohio"
2. Intro paragraph using `city.description`
3. CTABlock: "Get Your Free Quote in [City]"
4. Cost section: "How Much Do Replacement Windows Cost in [City]?"
5. Area highlights from `city.highlights`
6. FAQ component with city-specific questions
7. Bottom CTABlock

SEO per city:
- Title: `Window Replacement in ${city.name}, OH | Free Quote | Central Ohio Windows`
- Description: `Looking for window replacement in ${city.name}, Ohio? Get a free, no-obligation quote from a trusted local contractor. No pressure, no spam.`

**Step 3: Verify build**

Run: `npm run build`
Expected: Build succeeds, 14 city pages generated in `dist/`

Verify: `ls dist/ | grep ohio-windows`
Expected: 14 directories (columbus-ohio-windows, dublin-ohio-windows, etc.)

**Step 4: Commit**

```bash
git add src/data/cities.ts src/pages/\[city\]-ohio-windows.astro
git commit -m "feat: add 14 city landing pages with dynamic routes"
```

---

## Task 11: Build Replacement Window Cost Guide

> Use @frontend-design skill for visual quality

**Files:**
- Create: `src/pages/replacement-window-cost.astro`

**Step 1: Create the cost guide page**

A comprehensive pricing content page with:

1. H1: "How Much Do Replacement Windows Cost in Central Ohio?"
2. Intro: Overview of pricing ranges in the Central Ohio market
3. **Price table** by window type (use daisyUI `table` component):
   - Double Hung: $300–$700 per window
   - Casement: $350–$800
   - Bay/Bow: $1,200–$3,500
   - Picture: $250–$650
   - Sliding: $300–$700
   - Awning: $350–$750

4. **Cost factors section** — what affects price:
   - Window size and style
   - Frame material (vinyl, wood, fiberglass)
   - Glass type (double-pane, triple-pane, Low-E)
   - Number of windows
   - Labor and installation complexity
   - Permit requirements

5. **Average project cost** — "Most Central Ohio homeowners pay $8,000–$15,000 for a whole-house window replacement (10-15 windows)"

6. CTABlock: "Want an Exact Price for Your Home?"

7. Internal links to related content: Window Types, Energy Efficient Windows, How Replacement Works

SEO:
- Title: "Replacement Window Cost in Central Ohio (2025 Guide) | Central Ohio Windows"
- Description: "How much do replacement windows cost in Central Ohio? See average prices by window type, size, and material. Get a free quote for your home."

**Step 2: Verify build**

Run: `npm run build`
Expected: Build succeeds

**Step 3: Commit**

```bash
git add src/pages/replacement-window-cost.astro
git commit -m "feat: add replacement window cost guide page"
```

---

## Task 12: Build Window Types Guide

**Files:**
- Create: `src/pages/window-types.astro`

**Step 1: Create the window types page**

An educational guide covering each window type. For each type, include: description, best use cases, pros, cons, and price range.

Window types to cover:
1. Double Hung
2. Casement
3. Bay & Bow
4. Picture
5. Sliding
6. Awning
7. Hopper
8. Garden

Use daisyUI cards or a clean section layout for each type.

End with CTABlock: "Not Sure Which Window Type Is Right for You?"

SEO:
- Title: "Types of Replacement Windows | Central Ohio Homeowner's Guide"
- Description: "Learn about double hung, casement, bay, picture, and other window types. Find the best style for your Central Ohio home."

**Step 2: Verify build and commit**

```bash
npm run build && git add src/pages/window-types.astro && git commit -m "feat: add window types guide page"
```

---

## Task 13: Build Signs You Need New Windows Page

**Files:**
- Create: `src/pages/signs-you-need-new-windows.astro`

**Step 1: Create the page**

Content covering 7 signs:
1. Drafty rooms even with windows closed
2. Condensation between glass panes
3. Difficulty opening, closing, or locking windows
4. High energy bills
5. Excessive outside noise
6. Visible damage (rot, warping, cracks)
7. Windows are 20+ years old

Each sign: heading, description of the problem, why it matters, and what to do about it.

End with CTABlock.

SEO:
- Title: "7 Signs You Need New Windows | Central Ohio Windows"
- Description: "Drafty rooms? High energy bills? Learn the 7 warning signs that it's time to replace your windows."

**Step 2: Verify build and commit**

```bash
npm run build && git add src/pages/signs-you-need-new-windows.astro && git commit -m "feat: add signs-you-need-new-windows page"
```

---

## Task 14: Build Energy-Efficient Windows Page

**Files:**
- Create: `src/pages/energy-efficient-windows.astro`

**Step 1: Create the page**

Content covering:
- What makes a window energy efficient (Low-E glass, argon/krypton gas fill, multi-pane, frame material)
- Energy Star ratings explained
- U-Factor and SHGC explained simply
- Ohio-specific energy savings (heating-dominant climate, annual savings estimates)
- Available federal tax credits for energy-efficient windows
- Best energy-efficient window brands available in Central Ohio

End with CTABlock.

SEO:
- Title: "Energy-Efficient Windows for Central Ohio Homes | Save on Heating & Cooling"
- Description: "Learn how energy-efficient windows can lower your heating and cooling bills in Central Ohio. Understand Energy Star ratings, tax credits, and more."

**Step 2: Verify build and commit**

```bash
npm run build && git add src/pages/energy-efficient-windows.astro && git commit -m "feat: add energy-efficient windows page"
```

---

## Task 15: Build Vinyl vs. Wood Windows Page

**Files:**
- Create: `src/pages/vinyl-vs-wood-windows.astro`

**Step 1: Create the page**

Side-by-side comparison content:
- Overview of both materials
- Comparison table (use daisyUI `table`): cost, durability, maintenance, energy efficiency, aesthetics, lifespan
- Ohio climate considerations (temperature swings, humidity)
- Which is better for different situations
- Fiberglass as a third option (brief mention)

End with CTABlock.

SEO:
- Title: "Vinyl vs. Wood Windows: Which Is Best for Central Ohio? | Central Ohio Windows"
- Description: "Compare vinyl and wood replacement windows for Central Ohio homes. See costs, durability, maintenance, and which performs better in Ohio weather."

**Step 2: Verify build and commit**

```bash
npm run build && git add src/pages/vinyl-vs-wood-windows.astro && git commit -m "feat: add vinyl vs wood windows comparison page"
```

---

## Task 16: Build How Window Replacement Works Page

**Files:**
- Create: `src/pages/how-window-replacement-works.astro`

**Step 1: Create the page**

Step-by-step process guide:
1. Initial consultation and measurement
2. Choosing your windows (style, material, features)
3. Getting your quote
4. Scheduling installation
5. Installation day (what to expect, typical timeline: 1-2 days for a whole house)
6. Final inspection and cleanup
7. Warranty and follow-up

Include tips for homeowner preparation.

End with CTABlock: "Ready to Get Started?"

SEO:
- Title: "How Window Replacement Works: What to Expect | Central Ohio Windows"
- Description: "What happens during window replacement? From consultation to installation, learn the step-by-step process and what to expect."

**Step 2: Verify build and commit**

```bash
npm run build && git add src/pages/how-window-replacement-works.astro && git commit -m "feat: add how-window-replacement-works page"
```

---

## Task 17: Build About Page

**Files:**
- Create: `src/pages/about.astro`

**Step 1: Create the page**

Content:
- Mission: "We help Central Ohio homeowners find trusted window replacement contractors — for free."
- How it works (abbreviated version of HowItWorks, or import the component)
- Why we built this: "After seeing how overwhelming it can be to find a reliable window contractor, we created Central Ohio Windows as a free resource to simplify the process."
- Our promise: exclusive matching (one contractor, not five), privacy, no cost to homeowner
- Contact information or general inquiry form

SEO:
- Title: "About Central Ohio Windows | Your Window Replacement Resource"
- Description: "Central Ohio Windows is a free resource connecting homeowners with trusted local window contractors. Learn about our mission and how we work."

**Step 2: Verify build and commit**

```bash
npm run build && git add src/pages/about.astro && git commit -m "feat: add about page"
```

---

## Task 18: Add Privacy Policy Page

**Files:**
- Create: `src/pages/privacy-policy.astro`

**Step 1: Create the page**

Basic privacy policy covering:
- What information we collect (form submissions)
- How we use it (share with one local contractor for a quote)
- How we protect it (no selling to multiple parties, no spam)
- Contact for privacy questions

SEO:
- Title: "Privacy Policy | Central Ohio Windows"
- Description: "Read our privacy policy to understand how Central Ohio Windows protects your personal information."

**Step 2: Verify build and commit**

```bash
npm run build && git add src/pages/privacy-policy.astro && git commit -m "feat: add privacy policy page"
```

---

## Task 19: Internal Linking Pass and Final SEO Review

**Files:**
- Modify: All content pages

**Step 1: Add internal links between related content**

Ensure each content page links to related pages:
- Cost Guide → links to Window Types, Energy Efficient, How It Works
- Window Types → links to Cost Guide, Vinyl vs Wood
- Signs You Need → links to Cost Guide, How It Works, Free Quote
- Energy Efficient → links to Window Types, Cost Guide
- Vinyl vs Wood → links to Window Types, Cost Guide
- How It Works → links to Free Quote, Cost Guide
- City pages → link to Cost Guide, Window Types, Free Quote
- About → links to Free Quote, How It Works

**Step 2: Verify all pages have unique titles and descriptions**

Check that no two pages share the same `<title>` or meta description.

**Step 3: Verify build**

Run: `npm run build`
Expected: Build succeeds, all pages generated

Run: `ls -la dist/` to verify all pages exist.

**Step 4: Commit**

```bash
git add -A && git commit -m "feat: add internal linking across all content pages"
```

---

## Task 20: Final Build Verification and Visual Review

**Step 1: Full build**

Run: `npm run build`
Expected: Clean build, no warnings

**Step 2: Preview the site**

Run: `npm run preview`
Visit http://localhost:4321 and verify:
- Homepage renders with all sections
- Navigation works on all pages
- Lead capture form displays correctly
- All city pages render
- All content pages render
- Footer links work
- Mobile responsive layout works

**Step 3: Verify sitemap**

Check `dist/sitemap-index.xml` includes all pages.

**Step 4: Final commit if any fixes needed**

```bash
git add -A && git commit -m "fix: final build fixes and polish"
```

---

## Execution Notes

- **Tasks 1-7** build the foundation (theme + components). These should be completed first.
- **Task 8** (homepage) depends on Tasks 2-7 (all components).
- **Tasks 9-18** (individual pages) can be built in any order after the components exist, and can be parallelized across agents.
- **Task 10** (city pages) is the largest single task due to writing 14 sets of city-specific content.
- **Tasks 19-20** are final passes that depend on all pages being complete.
- Use @frontend-design skill for Tasks 2, 3, 6, 8, 11 to ensure high visual quality.
- All content should be factually accurate for Central Ohio — pricing data, climate references, and city details should be realistic.
