# Central Ohio Windows — Lead Generation Website Design

## Overview

Lead-generation website at centralohiowindows.com that captures homeowner info for window replacement projects and sells exclusive leads directly to one vetted window contractor per lead. Positioned as "Central Ohio's trusted window replacement resource" — an independent, helpful guide that connects homeowners with a trusted local professional.

## Key Differentiator

**Exclusive leads, not shared.** Unlike HomeAdvisor/Angi (which sell the same lead to 3-5 contractors), this site connects each homeowner with one contractor. Messaging emphasizes: "One contractor. One quote. Zero pressure." This is better for the homeowner (no flood of sales calls) and commands a premium price ($60-$150+ per lead).

## Target Geography

Broader Central Ohio region — Columbus metro + surrounding counties:
Columbus, Westerville, Dublin, Hilliard, Grove City, Worthington, Powell, Pickerington, Reynoldsburg, Delaware, Newark, Lancaster, Springfield, Mansfield

## Site Identity & Positioning

- **Brand:** Central Ohio Windows — Your Trusted Local Window Replacement Resource
- **Tone:** Helpful, knowledgeable, no-pressure
- **Trust signals:** "Free estimates" | "No obligation" | "One trusted local contractor" | "Your info stays private"
- **Not pretending to be a window company** — transparent about being a matching/resource service

## Page Structure (20+ pages)

### Core Pages
1. **Homepage** (`/`) — Hero CTA, how it works, value props, service areas, resources, FAQ
2. **Get a Free Quote** (`/free-quote`) — Primary lead capture form
3. **Replacement Window Cost Guide** (`/replacement-window-cost`) — Pricing data, cost factors
4. **Window Types Guide** (`/window-types`) — All window types with pros/cons/pricing
5. **Signs You Need New Windows** (`/signs-you-need-new-windows`) — 7 warning signs
6. **About** (`/about`) — Mission, how matching works

### City Landing Pages (14 pages, templated)
URL pattern: `/[city]-ohio-windows`
- Columbus, Delaware, Newark, Lancaster, Springfield, Mansfield
- Westerville, Dublin, Hilliard, Grove City, Worthington, Powell, Pickerington, Reynoldsburg

Each city page includes: city-specific H1, intro content, cost section, lead capture CTA, FAQ.

**Meta title pattern:** "Window Replacement in [City], OH | Free Quote | Central Ohio Windows"
**Meta description pattern:** "Looking for window replacement in [City], Ohio? Get a free, no-obligation quote from a trusted local contractor. No pressure, no spam."

### SEO Content Pages
7. **Vinyl vs. Wood Windows** (`/vinyl-vs-wood-windows`)
8. **Energy-Efficient Windows** (`/energy-efficient-windows`)
9. **How Window Replacement Works** (`/how-window-replacement-works`)

## Lead Capture Form Design

**Location:** Dedicated `/free-quote` page + inline CTAs on every other page.

**Fields (6):**
1. Full Name (text, required)
2. Phone Number (tel, required)
3. Email (email, required)
4. Street Address or ZIP Code (text, required)
5. Number of Windows (select: 1-3, 4-7, 8-12, 13+)
6. Project Timeline (select: ASAP, Within 1 month, 1-3 months, Just researching)

**CTA button:** "Get My Free Quote"
**Below form:** "Your information is safe. We only share it with one vetted local contractor."
**Form backend:** Netlify Forms (free tier: 100 submissions/month)

## Homepage Layout

1. **Nav bar** — Logo, page links, "Get Free Quote" button
2. **Hero** — H1: "Find a Trusted Window Replacement Pro in Central Ohio" / Sub: "Get a free, no-obligation quote from one vetted local contractor. No pressure, no spam." / CTA: "Get My Free Quote" / Trust badges
3. **How It Works** — 3 steps: Tell us about your project → We match you with the right pro → Get your free, no-pressure quote
4. **Why Homeowners Trust Us** — One contractor (not five), info stays private, 100% free
5. **Service Areas** — Grid of 14 cities with links
6. **Popular Resources** — Cards linking to content pages
7. **Inline CTA block** — Repeated lead capture prompt
8. **FAQ** — Common questions
9. **Footer** — All links, contact, privacy, disclaimer

## Reusable Components

- `Header` — nav bar with logo + links + CTA button
- `Footer` — site footer
- `HeroSection` — configurable hero (title, subtitle, CTA, background)
- `LeadCaptureForm` — 6-field Netlify form
- `CTABlock` — inline CTA used on content pages
- `HowItWorks` — 3-step visual process
- `FAQ` — accordion component
- `CityCard` — card for service area grid

## Technical Stack

- **Framework:** Astro v5 (static output, already configured)
- **Styling:** Tailwind CSS v4 + daisyUI v5 (already configured)
- **SEO:** astro-seo + @astrojs/sitemap (already configured)
- **Forms:** Netlify Forms (no backend needed)
- **Hosting:** Netlify (implied by form choice)
- **Design:** Blue/white professional color scheme, icon-based (no stock photos at launch)

## Competitive Research Summary

### Lead-Gen Competitors on These Search Terms

| Company | Model | Page Title Pattern |
|---------|-------|--------------------|
| HomeAdvisor/Angi | Shared leads $15-$100 | "Top-Rated Window Services Experts in [City], OH" |
| Modernize | Shared leads $60-$150 | "How Much Does Window Replacement Cost in [State]?" |
| CraftJack | Shared leads $35-$80 | "Window Leads, Installation & Replacement Leads" |
| HomeBlue | Referral | "Window Replacement Cost in [City], [State]" |
| Exterior Heroes | Quote funnels | "[State] Window Cost Calculator" |
| windowreplacementcolumbusohio.com | GoHighLevel lead-gen | "Window Replacement Columbus Ohio \| Expert Installation" |

### Patterns That Convert
- Multi-step forms outperform single forms
- Cost calculators/quizzes provide value before asking for info
- 3-5 fields maximize conversion; each additional field drops conversion 10-20%
- "Free estimate/quote" is the universal CTA language
- Phone numbers with click-to-call capture 30-40% of prospects
- Trust signals above the fold: reviews, certifications, privacy promises
- Exclusive lead positioning differentiates from aggregators

## SEO Strategy

- Domain advantage: centralohiowindows.com exactly matches target search terms
- City-specific pages target "[city] window replacement" long-tail keywords
- Content pages target research-phase queries (cost, types, signs, comparisons)
- Each page has unique title, description, H1 targeting specific keywords
- Internal linking between content pages and city pages
- Sitemap auto-generated by Astro
