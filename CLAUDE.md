# CLAUDE.md — Fulcrum Advisory
## Complete Build Guide for Claude Code

> Read this file entirely before touching anything. It is the single source of truth.
> When in doubt: look at what's already built and match it exactly.

---

## 1. Project Overview

**Client:** David Taylor — Principal, Fulcrum Advisory
**Site purpose:** Professional services website for a cleared GovCon advisor. Must look like it has been operating for several years. PwC-caliber polish.
**Hosting:** GitHub Pages — 100% static. No server-side code, no build tools, no frameworks.
**Domain:** `fulcrumadvisory.us`
**Primary contact:** `info@fulcrumadvisory.us`

### David's Unique Position (understand this before writing a single word of copy)
David is one of a handful of people in the US who combines:
- **FOCI**: 16+ years *inside* a FOCI-mitigated contractor (Leonardo Electronics US). Has personally run DCSA engagements, SF 328 filings, SSA maintenance, and mitigation agreement cycles. Billed $350/hr for SSA work 10+ years ago.
- **CMMC**: Built and maintained SSPs, POA&Ms, and NIST 800-171 compliance programs under live DCSA scrutiny.
- **AI in GCC High**: Designed and deployed a production enterprise AI assistant (Azure OpenAI + RAG + CosmosDB + Bot Framework) inside a CMMC-scoped GCC High tenant. This is not a POC — it runs in production.
- **Active U.S. Security Clearance**: Real accountability. Not a talking point.

Copy must convey practitioner credibility, not consultant-speak. Every sentence should pass the test: *would someone who has actually done this write it this way?*

---

## 2. Aesthetic Direction — PwC-Caliber, Defense-Authoritative

Study `styles.css` before writing any HTML. The design system is fully defined there.

### The Look
Think PwC or Booz Allen Hamilton — not a startup, not a agency portfolio. Established. Authoritative. Typography-led. Restrained use of color. Generous white space. Zero visual clutter.

- **Dark navy backgrounds** for hero, nav, footer, and CTA sections
- **White/off-white** for content sections  
- **Gold accents** (`#C8962E`) for eyebrow labels, rule lines, hover states, and CTAs — used *sparingly*
- **No photography** — geometric grid overlays, rule lines, and typography carry the visual weight
- **No gradients** except very subtle overlays
- **No rounded corners** larger than `4px` — this is precise, not friendly

### Typography Hierarchy (from `styles.css`)
| Role | Font | Weight |
|---|---|---|
| Headings / Display | Libre Baskerville | 700 (italic for emphasis) |
| Body / UI | Nunito Sans | 300, 400, 600, 700 |
| Code / Framework refs | IBM Plex Mono | 400, 500 |

Always load: `https://fonts.googleapis.com/css2?family=Libre+Baskerville:ital,wght@0,400;0,700;1,400&family=Nunito+Sans:wght@300;400;600;700&family=IBM+Plex+Mono:wght@400;500&display=swap`

### CSS Variables (defined in styles.css — never hardcode these values)
```
--navy: #0A1628          --gold: #C8962E
--navy-mid: #122040      --gold-light: #DDAA45
--navy-light: #1B3560    --gold-pale: #F5EDD8
--blue: #1B4F8A          --white: #FFFFFF
--blue-light: #2563A8    --off-white: #F7F8FA
--text: #111827          --border: #E5E7EB
--text-mid: #374151      --font-serif: Libre Baskerville
--text-muted: #6B7280    --font-sans: Nunito Sans
                         --font-mono: IBM Plex Mono
```

---

## 3. File Structure — Complete

```
fulcrumadvisory.us/
│
├── CLAUDE.md                    ← This file
├── styles.css                   ← ✅ BUILT — global design system, do not modify
├── sitemap.xml                  ← ✅ BUILT
├── robots.txt                   ← ✅ BUILT
├── CNAME                        ← ✅ BUILT — fulcrumadvisory.us
├── 404.html                     ← ✅ BUILT
│
├── index.html                   ← ✅ BUILT — homepage
├── about.html                   ← ✅ BUILT — firm bio and credentials (firm-level, no personal name)
├── contact.html                 ← ✅ BUILT — contact form + Microsoft Bookings embed
├── services.html                ← ✅ BUILT — 6 services overview
├── insights.html                ← ✅ BUILT — article index (9 articles)
├── privacy.html                 ← ✅ BUILT
├── terms.html                   ← ✅ BUILT
│
├── services/
│   ├── foci-advisory.html       ← ✅ BUILT
│   ├── cmmc-compliance.html     ← ✅ BUILT
│   ├── ai-govcon.html           ← ✅ BUILT
│   ├── gcch-platforms.html      ← ✅ BUILT — GCC High Platform Solutioning (5 capabilities)
│   ├── corp-comms.html          ← ✅ BUILT — Corporate Communications (NEW)
│   └── vciso-advisory.html      ← ✅ BUILT
│
├── insights/
│   ├── dfars-foci-rule-2026.html          ← ✅ BUILT — May 25, 2026 (Section 847 rule)
│   ├── dfars-foci-rule-2025.html          ← ✅ BUILT — May 12, 2025
│   ├── ai-cmmc-gcc-high.html             ← ✅ BUILT — March 3, 2025
│   ├── cmmc-final-rule-2024.html         ← ✅ BUILT — January 14, 2025
│   ├── nist-800-171-rev3.html            ← ✅ BUILT — November 7, 2024
│   ├── foci-foreign-investment-risk.html  ← ✅ BUILT — September 18, 2024
│   ├── gcc-high-ai-architecture.html     ← ✅ BUILT — July 22, 2024
│   ├── cmmc-scope-common-mistakes.html   ← ✅ BUILT — April 9, 2024
│   └── dcsa-assessment-prep.html         ← ✅ BUILT — January 30, 2024
│
└── assets/
    ├── favicon.svg               ← 🔲 Inline SVG favicon (pending)
    └── og-image.png              ← 🔲 Skip — not required for GitHub Pages launch
```

---

## 4. Page-by-Page Build Specifications

### 4.1 Nav & Footer Pattern
Every page must use the identical nav and footer. Copy it exactly from `index.html`. Only change:
- The `class="active"` on the correct nav link
- The page's `<title>`, `<meta name="description">`, `<link rel="canonical">`

**Nav behavior:**
- Fixed top, `z-index: 1000`
- Adds `.scrolled` class (box-shadow) after 40px scroll — handled by inline `<script>` at bottom of every page
- Gold "Schedule a Call" button always visible on desktop
- Hamburger + full-screen overlay on mobile

**Footer columns:** Brand+contact | Services | Insights | Company

---

### 4.2 `services.html` — Services Overview

**Page header:** Dark navy, grid overlay, breadcrumb (Home / Services)
- H1: "Our Services"
- Subhead: "Fixed-scope engagements, advisory retainers, and project-based work — all delivered by David Taylor directly."

**Body layout:** Four full-width service sections, alternating white/off-white background. Each section:
```
[Left: number + heading + description + engagement details]
[Right: package pricing card with specifics]
```

**The four services:**

**01 — FOCI Advisory**
- Problem: "The May 2025 DFARS proposed rule means 40,000 contractors who have never touched classified work may now face SF 328 filings, beneficial ownership disclosure, and 90-day mitigation timelines triggered by option exercises and contract modifications."
- What David delivers: Initial FOCI risk assessment, SF 328 preparation and review, DCSA engagement strategy, SSA/mitigation agreement navigation, beneficial ownership structure analysis, ongoing retainer support through the mitigation lifecycle
- Packages table:

| Engagement | Scope | Price |
|---|---|---|
| FOCI Readiness Assessment | Ownership structure review, DFARS applicability analysis, SF 328 preparation guidance, written findings | $4,500 |
| FOCI Mitigation Advisory | Full SSA/proxy/voting trust strategy, DCSA engagement support, documentation package | Contact for scope |
| Ongoing FOCI Retainer | Continuous compliance monitoring, contract action reviews, annual recertification support | From $4,000/mo |

**02 — CMMC Compliance**
- Problem: "32 CFR Part 170 took effect December 16, 2024. CMMC Level 2 certification is now a contract requirement for defense contractors handling CUI. Most contractors significantly underestimate their scoping and remediation burden."
- What David delivers: CUI scoping and data flow analysis, NIST SP 800-171 Rev 3 gap assessment, SSP development, POA&M creation and tracking, C3PAO assessment preparation, policy and procedure drafting
- Packages table:

| Engagement | Scope | Price |
|---|---|---|
| CMMC L2 Gap Assessment | Full 110-control assessment, scoping analysis, written gap report | $4,000–6,500 |
| SSP + POA&M Development | Complete System Security Plan and Plan of Action & Milestones | $6,000–10,000 |
| C3PAO Assessment Prep | Evidence package, interviewing, mock assessment | $5,000–8,000 |
| CMMC L3 Advisory | DIBCAC engagement prep, enhanced controls gap analysis | Contact for scope |

**03 — AI in GCC High**
- Problem: "Leadership is demanding AI adoption. Your compliance officer is demanding you don't blow up the CMMC boundary. Most AI vendors will tell you their tool is 'FedRAMP authorized' and call it a day. That's not an SSP entry. It's not a boundary definition. And it won't survive a CMMC audit."
- What David delivers: AI use case scoping against CMMC boundary, GCC High architecture design (Azure OpenAI, AI Search, CosmosDB), production deployment and configuration, SSP amendment for AI components, acceptable use policy and data handling SOP, model governance documentation
- Packages table:

| Engagement | Scope | Price |
|---|---|---|
| AI Readiness Assessment | Use case inventory, CUI boundary analysis, GCC High compatibility audit, written report | $3,500–5,000 |
| GCC High AI Deployment | Full architecture, deployment, and configuration of Azure OpenAI + RAG in client tenant | $10,000–18,000 |
| AI Policy Package | Acceptable use policy, data handling SOP, SSP amendment, risk register entries | $2,500–3,500 |

**04 — Fractional vCISO**
- Problem: "A cleared defense contractor CISO costs $250,000–350,000/year in salary and benefits, doesn't exist in the labor market anyway, and is overkill for a 75-person company whose primary compliance challenge is CMMC and FOCI — not a 24/7 SOC."
- What David delivers: Security program ownership and strategy, board and leadership reporting, vendor and tool evaluations, incident response planning, DCSA/auditor interface, compliance calendar management, staff advisory
- Packages: From $5,000/month | Minimum 3-month engagement | Scoped to client need

**Bottom CTA:** "All engagements are delivered by David Taylor personally. No subcontractors, no junior analysts, no bait-and-switch. [Schedule a Call]"

---

### 4.3 `services/foci-advisory.html` (and the other three service detail pages)

Deep-dive pages. Structure:
1. Dark page header with breadcrumb (Home / Services / FOCI Advisory)
2. Problem statement section — long-form, detailed, authoritative
3. "What We Do" — detailed deliverables
4. "How It Works" — 3-step engagement process
5. Package pricing table
6. FAQ section (3–5 questions relevant to that service)
7. CTA callout block

**FOCI page FAQs:**
- "Does the DFARS proposed rule affect my existing contracts?" → Yes — option exercises and modifications on existing contracts count as contract actions that trigger the timeline.
- "What's the difference between an SSA, proxy agreement, and voting trust?" → Brief accurate explanations of each mitigation type.
- "How long does DCSA FOCI mitigation typically take?" → Depends on structure; SSAs can be faster; proxies and voting trusts take longer. David has navigated all three.
- "Do I need a lawyer or just a consultant?" → Both, typically. David's role is the technical/operational FOCI compliance piece; legal counsel handles the corporate structure side. He can recommend FOCI-experienced counsel.

---

### 4.4 `insights.html` — Article Index

**Layout:** Two-column article grid (3 per row on desktop, 1 on mobile)
**Filter tabs:** All | FOCI | CMMC | AI & Cloud | Strategy

**All 8 articles listed with:** date, category tag, title, 2-sentence excerpt, read time, "Read article →"

**Article index (newest first):**

| # | Date | Category | Title |
|---|---|---|---|
| 1 | May 12, 2025 | FOCI · Regulatory | What the New DFARS FOCI Rule Means for 40,000 Defense Contractors |
| 2 | March 3, 2025 | AI · GCC High · CMMC | Deploying AI Inside a CMMC Boundary Without Destroying Your Compliance Posture |
| 3 | January 14, 2025 | CMMC · Compliance | CMMC Final Rule Is Live: The Clock Is Running for 80,000 Contractors |
| 4 | November 7, 2024 | CMMC · NIST | NIST SP 800-171 Rev 3 Is Final: What Changed and What It Means for Your SSP |
| 5 | September 18, 2024 | FOCI · Strategy | Foreign Investment in Defense Contractors: What Triggers FOCI and What Doesn't |
| 6 | July 22, 2024 | AI · Cloud | GCC High vs. Commercial Azure: Why the Boundary Matters More Than the Vendor |
| 7 | April 9, 2024 | CMMC · Compliance | The Five Scoping Mistakes That Sink CMMC Assessments Before They Start |
| 8 | January 30, 2024 | FOCI · DCSA | How to Prepare for a DCSA FOCI Review: What They Actually Look At |

---

### 4.5 Blog Post Template (all 8 articles)

Every article page uses this structure:

```html
<!-- Dark article header -->
<div class="article-header">
  <div class="container container--narrow">
    [breadcrumb: Home / Insights / Article Title]
    <div class="article-meta">
      <span class="article-tag">CATEGORY</span>
      <span class="article-date">Month DD, YYYY · N min read</span>
    </div>
    <h1>[Article Title]</h1>
    <p class="article-sub">[One sentence that is the sharpest possible version of the article's thesis]</p>
    <div class="article-author">
      <div class="author-avatar">DT</div>
      <div class="author-info">
        <div class="author-name">David Taylor</div>
        <div class="author-role">Principal · Fulcrum Advisory</div>
      </div>
    </div>
  </div>
</div>

<!-- Article body -->
<div class="article-body">
  [H2 / H3 / p / ul / ol — full article content]

  <!-- Mid-article CTA -->
  <div class="article-cta">
    <h3 style="color:var(--white)">Dealing with [topic]?</h3>
    <p style="color:rgba(255,255,255,0.65)">David Taylor works directly with defense contractors on [topic]. [One sentence on what he delivers.]</p>
    <a href="../contact.html" class="btn btn--gold">Schedule a Call</a>
  </div>

  [remaining article content]
</div>

<!-- Related articles (2–3 cards) -->
<section class="section section--gray">
  <div class="container">
    <span class="eyebrow">Related Insights</span>
    <h2>Continue Reading</h2>
    [2-3 insight-card components linking to related articles]
  </div>
</section>
```

---

### 4.6 Blog Post Content — Write All 8 Articles in Full

Each article must be **800–1,400 words**, written in David's voice: direct, practitioner-level, no-fluff. Reference specific regulation numbers, DCSA processes, NIST control families, Azure service names. This is what makes the site look established and authoritative.

**Article 1 — `dfars-foci-rule-2025.html`**
Date: May 12, 2025 | Tags: FOCI, Regulatory

Cover: What the May 7, 2025 DFARS proposed rule actually says. Which contract vehicles it covers (unclassified over $5M). What "contract action" means and why option exercises and modifications are traps most companies will miss. The SF 328 filing requirement. Beneficial ownership disclosure. The 90-day mitigation clock. What contractors should do right now (ownership structure audit, legal counsel, FOCI advisor engagement before the next contract action). Comments close July 6, 2025.

**Article 2 — `ai-cmmc-gcc-high.html`**
Date: March 3, 2025 | Tags: AI, GCC High, CMMC

Cover: The three decisions that determine compliance before any code is written: (1) Does the AI system touch, process, or store CUI? (2) Is your Azure tenant GCC High, not commercial? (3) Have you amended your SSP to include the AI components? Then: Why "FedRAMP authorized" isn't the same as "in your authorization boundary." Azure OpenAI in GCC High — what's available and what's not vs. commercial. RAG architecture and CUI data handling. Model logging and audit trail requirements. What a CMMC auditor will actually ask about your AI system.

**Article 3 — `cmmc-final-rule-2024.html`**
Date: January 14, 2025 | Tags: CMMC, Compliance

Cover: 32 CFR Part 170 effective December 16, 2024. What actually changed from CMMC 2.0. The phased rollout timeline (Phase 1 through Phase 4). What "CMMC Level 2 Certification" now means contractually. Difference between self-assessment (L1, some L2) and C3PAO assessment (L2 conditional, L3). The SPRS score requirement. What your first 90 days should look like: scoping, gap assessment, SSP triage, POA&M development.

**Article 4 — `nist-800-171-rev3.html`**
Date: November 7, 2024 | Tags: CMMC, NIST

Cover: Rev 3 added 17 new requirements (now 110 total), reorganized control families, and introduced "organization-defined parameters." Key changes to AC, AU, CM, IR, and SA families. What "ODP" means for SSP authors — it's not a blank check, DCSA will scrutinize your defined parameters. How to update an existing SSP. Common Rev 3 gaps in legacy SSPs.

**Article 5 — `foci-foreign-investment-risk.html`**
Date: September 18, 2024 | Tags: FOCI, Strategy

Cover: What actually constitutes FOCI — the four vectors (ownership, control, influence, access). Common ownership structures that trigger FOCI: foreign parent companies, foreign-national board members, foreign-controlled private equity. What doesn't automatically trigger FOCI. The NID (National Interest Determination) pathway. How FOCI interacts with facility clearances and personnel security. Why the corporate transaction team at your PE firm needs to call a FOCI advisor before closing, not after.

**Article 6 — `gcc-high-ai-architecture.html`**
Date: July 22, 2024 | Tags: AI, Cloud

Cover: GCC High vs. commercial Azure — the actual technical differences that matter for compliance. Data residency. The Microsoft Graph endpoint differences. Which Azure AI services are available in GCC High (Azure OpenAI: yes. Azure AI Search: yes. Some cognitive services: no). Architecture pattern for a compliant RAG deployment: Azure OpenAI + Azure AI Search + CosmosDB + Entra ID authentication. The SSP system boundary diagram you need to draw before you write any code. Network security group and private endpoint requirements.

**Article 7 — `cmmc-scope-common-mistakes.html`**
Date: April 9, 2024 | Tags: CMMC, Compliance

Cover: The five scoping mistakes:
1. Treating "CUI environment" as "everything" — scoping too broad makes the assessment unmanageable
2. Forgetting contractor-managed external services — your cloud backup provider is in scope if it touches CUI
3. Missing "security protection assets" — systems that protect CUI are in scope even if they don't touch it
4. Not documenting CUI flows — if you can't draw the data flow, you can't defend the boundary
5. Treating the SSP as a one-time document — it's a living document; every system change is a SSP change

**Article 8 — `dcsa-assessment-prep.html`**
Date: January 30, 2024 | Tags: FOCI, DCSA

Cover: What DCSA actually looks at during a FOCI review. The difference between an initial FOCI determination and an ongoing compliance review. Key documents they'll want: SF 328, corporate organizational charts, board meeting minutes, foreign contact reports, beneficial ownership records. The most common findings (board composition, foreign national access, inadequate visitor logs). How to conduct a pre-assessment internal review. What happens if DCSA finds a problem — the remediation timeline and mitigation options.

---

### 4.7 `privacy.html` and `terms.html`

Both are clean, minimal, legal-language pages. Dark page header. Body text in narrow container. Standard professional services language.

**privacy.html:** What data is collected (contact form submissions, no tracking cookies beyond basic analytics if added later), how it's used (to respond to inquiries), no data sold or shared, contact for data requests.

**terms.html:** Services are provided by Fulcrum Advisory as independent advisory. No attorney-client, no securities advice, no guarantee of regulatory outcomes. Governing law: state of [David to confirm]. Limitation of liability to fees paid in the prior 90 days.

---

### 4.8 `404.html`

Dark navy page, centered. TCS logo. "404 — Page Not Found." One line: "The page you're looking for doesn't exist or may have moved." Two buttons: [Back to Home] and [Contact Us].

---

### 4.9 `sitemap.xml`

Standard XML sitemap. Include all pages with:
- `<loc>`: full canonical URL
- `<lastmod>`: use realistic dates (index.html = today, articles = their publish date)
- `<changefreq>`: monthly for static pages, weekly for insights index
- `<priority>`: 1.0 for index, 0.9 for services, 0.8 for insights, 0.7 for individual articles

---

### 4.10 `robots.txt`

```
User-agent: *
Allow: /
Sitemap: https://www.fulcrumadvisory.us/sitemap.xml
```

---

### 4.11 `CNAME`

Single line, no trailing newline:
```
fulcrumadvisory.us
```

---

## 5. Contact Form Implementation

The contact form in `contact.html` is a **placeholder** matching the same solution David used for his Paradise Beach House website. Do not implement a different form backend. The form HTML is already in place with correct field IDs and names.

**What Claude Code should do:** Leave the form HTML exactly as-is. Add a comment block above the form clearly marking where the form handler script should be inserted. The `<form>` element should have `id="contact-form"` so any handler can target it consistently.

**Calendly embed:** The `<div id="calendly-embed">` placeholder is already in `contact.html`. When David provides his Calendly URL, replace the placeholder div with the official Calendly inline embed:
```html
<div class="calendly-inline-widget"
     data-url="https://calendly.com/DAVID_SLUG/30min"
     style="min-width:320px;height:630px;">
</div>
<script type="text/javascript" src="https://assets.calendly.com/assets/external/widget.js" async></script>
```

---

## 6. SEO Implementation — Applied to Every Page

### Meta tags (required on every page)
```html
<title>[Page Title] | Fulcrum Advisory</title>
<meta name="description" content="[150–160 char description with primary keyword]" />
<meta name="keywords" content="[5–10 relevant keywords]" />
<meta name="author" content="David Taylor" />
<meta name="robots" content="index, follow" />
<link rel="canonical" href="https://www.fulcrumadvisory.us/[path]" />

<!-- Open Graph -->
<meta property="og:type" content="[website or article]" />
<meta property="og:title" content="[Page title]" />
<meta property="og:description" content="[Same as meta description]" />
<meta property="og:url" content="https://www.fulcrumadvisory.us/[path]" />
<meta property="og:site_name" content="Fulcrum Advisory" />

<!-- Twitter -->
<meta name="twitter:card" content="summary_large_image" />
<meta name="twitter:title" content="[Page title]" />
<meta name="twitter:description" content="[Description]" />
```

### Schema.org (structured data — apply per page type)

**Blog articles** — use `Article` schema:
```json
{
  "@context": "https://schema.org",
  "@type": "Article",
  "headline": "[Article title]",
  "description": "[Article description]",
  "datePublished": "[YYYY-MM-DD]",
  "dateModified": "[YYYY-MM-DD]",
  "author": {
    "@type": "Person",
    "name": "David Taylor",
    "url": "https://www.fulcrumadvisory.us/about.html"
  },
  "publisher": {
    "@type": "Organization",
    "name": "Fulcrum Advisory",
    "url": "https://www.fulcrumadvisory.us"
  },
  "mainEntityOfPage": "https://www.fulcrumadvisory.us/insights/[slug].html"
}
```

**Service pages** — use `Service` schema:
```json
{
  "@context": "https://schema.org",
  "@type": "Service",
  "name": "[Service Name]",
  "provider": {
    "@type": "ProfessionalService",
    "name": "Fulcrum Advisory"
  },
  "description": "[Service description]",
  "areaServed": "United States",
  "audience": { "@type": "Audience", "audienceType": "Defense Contractors" }
}
```

### Keyword targeting (use naturally in headings and body copy)

**Primary:** FOCI advisory, CMMC compliance consultant, CMMC Level 2 assessment, GCC High AI deployment, defense contractor cybersecurity, vCISO GovCon

**Secondary:** SF 328 filing, DCSA FOCI, FOCI mitigation agreement, SSA consultant, NIST SP 800-171, POA&M development, fractional CISO defense contractor, Azure OpenAI GCC High, CMMC final rule 2024, DFARS FOCI rule 2025

**Long-tail (use in article headings and body):** "how to prepare for DCSA FOCI review", "AI deployment CMMC compliant", "FOCI mitigation agreement types", "CMMC Level 2 gap assessment cost", "GCC High vs commercial Azure compliance"

### Internal linking rules
- Every service detail page links to `contact.html` and `services.html`
- Every article links to at least one relevant service page
- Insights index links to all 8 articles
- Every page links to at least 2–3 other pages (nav links count)
- Use descriptive anchor text, not "click here"

---

## 7. Hard Rules for Claude Code

1. **`styles.css` is sacred.** Do not modify it. Do not add inline styles that duplicate or conflict with it. Use CSS custom properties throughout.

2. **No frameworks.** No Bootstrap, Tailwind, React, Vue, jQuery, or any external library except Google Fonts and the Calendly embed script. Vanilla HTML/CSS/JS only.

3. **No lorem ipsum.** Every word of copy must be real, based on this CLAUDE.md. If something is genuinely unknown (e.g., David's LinkedIn URL), use `href="#" data-placeholder="true"` and add an HTML comment.

4. **All paths are relative.** No leading slash on asset paths — GitHub Pages with a custom domain will break if you use absolute paths. Use `../styles.css` from subdirectory pages.

5. **Nav active state.** The correct nav link must have `class="active"` on every page.

6. **Breadcrumbs on every interior page.** Use correct hierarchy. Links must work.

7. **Every page has a canonical URL.** No exceptions.

8. **All article dates are real industry event dates.** The articles are backdated to correspond to actual FOCI/CMMC/NIST events. Do not change them.

9. **Pricing is shown as ranges, never exact.** Never show an hourly rate on the public site. Packages show "From $X" or "$X–$Y" ranges. Hourly advisory is available but discussed privately.

10. **Mobile first.** Test every page at 375px width mentally. If it won't work on mobile, fix it before moving on.

11. **Performance.** No unoptimized images. No render-blocking scripts (put all `<script>` tags at end of `<body>`). Google Fonts loaded with `display=swap`.

12. **Accessibility.** All images have `alt` text. Form inputs have `<label>`. Buttons have `aria-label` when icon-only. Color contrast meets WCAG AA.

---

## 8. Open Items (David to Confirm)

| Item | Status | Notes |
|---|---|---|
| Calendly URL | ⏳ Pending | Insert into `contact.html` `#calendly-embed` |
| LinkedIn URL | ⏳ Pending | Footer + about.html `data-placeholder="true"` |
| Contact form backend | ⏳ Pending | Same solution as Paradise Beach House website |
| State of incorporation | ⏳ Pending | Needed for `terms.html` |
| Any certifications (CISSP, etc.) | ⏳ Pending | Add to `about.html` credential cards |
| Logo/favicon preference | ⏳ Pending | Currently text-based; SVG monogram "TCS" acceptable |
| Google Analytics / Search Console | ⏳ Pending | Add `<script>` tag to `<head>` of all pages when ready |

---

## 9. Current Build Status

| File | Status |
|---|---|
| `styles.css` | ✅ Complete |
| `index.html` | ✅ Complete |
| `about.html` | ✅ Complete |
| `contact.html` | ✅ Complete |
| `services.html` | 🔲 Build next |
| `services/foci-advisory.html` | 🔲 |
| `services/cmmc-compliance.html` | 🔲 |
| `services/ai-govcon.html` | 🔲 |
| `services/vciso-advisory.html` | 🔲 |
| `insights.html` | 🔲 |
| `insights/dfars-foci-rule-2025.html` | 🔲 |
| `insights/ai-cmmc-gcc-high.html` | 🔲 |
| `insights/cmmc-final-rule-2024.html` | 🔲 |
| `insights/nist-800-171-rev3.html` | 🔲 |
| `insights/foci-foreign-investment-risk.html` | 🔲 |
| `insights/gcc-high-ai-architecture.html` | 🔲 |
| `insights/cmmc-scope-common-mistakes.html` | 🔲 |
| `insights/dcsa-assessment-prep.html` | 🔲 |
| `privacy.html` | 🔲 |
| `terms.html` | 🔲 |
| `404.html` | 🔲 |
| `CNAME` | 🔲 |
| `robots.txt` | 🔲 |
| `sitemap.xml` | 🔲 (build last) |
