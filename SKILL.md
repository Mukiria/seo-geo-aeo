---
name: seo-geo-aeo
description: Audit and improve a website's visibility in traditional search (SEO), AI-generated answers (GEO), and answer boxes/voice/featured snippets (AEO). Use when the user asks for an SEO audit, keyword or content strategy, technical SEO fixes, structured data, llms.txt, AI-search visibility, or SEO-optimized copy.
---

# SEO + GEO + AEO Skill

## Purpose

Help a site get found, understood, and cited, in three places:

- **SEO (Search Engine Optimization):** rank in classic results (Google, Bing).
- **AEO (Answer Engine Optimization):** win featured snippets, "People also ask", knowledge panels, and voice answers by answering questions directly.
- **GEO (Generative Engine Optimization):** get mentioned and cited inside AI answers (ChatGPT, Claude, Perplexity, Gemini, Google AI Overviews, Copilot).

The three share one foundation: **crawlable pages, clear entities, direct answers, and trustworthy sources.** Do the foundation first.

## Ground rules (honesty and evidence)

1. **Separate what you observed from what you inferred.** Say which files, pages, or tools you actually checked. Never present a guess as a finding.
2. **Never fabricate metrics** (rankings, traffic, search volume, Core Web Vitals scores). If you don't have the data, say what tool would produce it.
3. **No guarantees.** Nobody can promise rankings or AI citations. Frame work as improving eligibility and clarity.
4. **Flag unverified practices.** Some GEO tactics (e.g. `llms.txt`) have no confirmed effect from major engines. Label them low-cost / unproven.
5. **Fix in priority order.** Indexability, then content and intent, then enhancements. Don't polish titles on a page crawlers can't read.
6. **Don't recommend spam**: keyword stuffing, hidden text, fake reviews, doorway pages, paid link schemes, mass AI-generated filler.
7. **Re-check time-sensitive claims.** Search-engine and AI-vendor behavior changes. Crawler user-agent names, which rich results Google still shows (e.g. FAQ), whether AI crawlers execute JavaScript, and the status of `llms.txt` were last reviewed in this file on 2026-10-25 from the text alone, not re-verified against vendor docs. Before relying on one in an audit, confirm it in the vendor's current documentation, and say when you couldn't.

## Workflow

Follow these phases in order. Skip a phase only if the user gives you its result.

**Match the workflow to the request.** If the user wants only copy, schema, keyword strategy, or `llms.txt` (no site to crawl), run Phase 1 for the facts you need plus the relevant phase, and don't run a full audit. If a live site is available but the user didn't ask for a full audit, use the quick audit format below.

### Phase 1: Intake
Collect or confirm: domain, business type, target audience and country/region, primary services/products, top 5-10 target queries (or help derive them), competitors, and what access exists (Search Console, Analytics, CMS, developer).

### Phase 2: Crawlability and indexability (blocking issues)
Check in this order:

- [ ] Does the page return real content in the HTML crawlers receive? (Raw `curl` / view-source / "Test Live URL" in Search Console, not the rendered DOM from a browser tool. Client-side rendered SPAs often return an empty shell.)
- [ ] robots.txt: not blocking important paths, references the sitemap, admin/private paths disallowed.
- [ ] `<meta name="robots">` and `X-Robots-Tag`: no accidental `noindex`/`nofollow`.
- [ ] HTTP status: 200 for live pages, 301 for moves, 404/410 for gone. No soft 404s (SPA returning 200 for missing routes).
- [ ] Canonicals: one self-referencing canonical per page; consistent `www` vs non-`www`, `http` vs `https`, trailing slash.
- [ ] HTTPS everywhere; no mixed content.
- [ ] Multi-language or multi-region sites: `hreflang` annotations are reciprocal, include a self-reference and `x-default`, and use valid language/region codes; each language version has its own self-canonical.
- [ ] Internal links are real `<a href>` links (not click handlers only).
- [ ] Sitemap: valid XML, lists all indexable URLs, includes accurate `<lastmod>`. (`priority` and `changefreq` are largely ignored by Google.)
- [ ] No important content hidden behind logins, tabs that load on click only, or infinite scroll without paginated URLs.

**Checks you can run yourself** (report only what you actually ran):

- Raw HTML as crawlers get it: `curl -sL -A "Googlebot" <url>`. Browser tools return the rendered DOM, which can hide an empty shell, so use `curl` or view-source for this check.
- Status, redirects and headers: `curl -sIL <url>` (look for the redirect chain, `X-Robots-Tag`, and `http` → `https` and `www` handling).
- Soft 404: `curl -sI <url>/this-page-should-not-exist-12345` should return 404, not 200.
- `curl -s <domain>/robots.txt` and `curl -s <domain>/sitemap.xml`; confirm the sitemap URLs return 200 and match the canonical host.
- Canonical and robots meta: `curl -s <url> | grep -iE 'rel="canonical"|name="robots"'`.

**If the site is a JavaScript SPA (React/Vue/Vite):** recommend server-side rendering, static generation, or prerendering per route. Do not treat this as optional.

### Phase 3: Technical performance and UX
- Core Web Vitals (LCP, INP, CLS): measure with PageSpeed Insights / CrUX. Don't estimate. Low-traffic sites often have no CrUX field data; in that case use Lighthouse lab data and label it as lab, not field, data.
- Mobile-friendly layout and readable tap targets.
- Image optimization: modern formats (WebP/AVIF), explicit width/height, lazy-load below the fold.
- JS bundle size, render-blocking resources, caching and compression.

### Phase 4: On-page SEO
For every important page:

- **Title tag:** ~50-60 characters, primary topic first, brand last (or first on the homepage). Unique per page. No decorative symbols.
- **Meta description:** ~140-160 characters, a clear benefit plus a reason to click. Not a ranking factor, but it affects click-through.
- **One H1** that matches the page's main intent; logical H2/H3 hierarchy.
- **URL:** short, lowercase, hyphenated, descriptive.
- **Opening paragraph** states what the page is and who it's for within the first ~100 words.
- **Images:** descriptive filenames and alt text that describes the image, not keywords stuffed in. Include important images in the sitemap (image extension) or in crawlable `<img>` tags, not CSS backgrounds only.
- **Target region and language:** write for the audience's country (spelling, currency, local terms, payment methods and locations), set `<html lang>`, and use `hreflang` if serving more than one language or region.
- **Internal links:** descriptive anchor text, linking related pages (hub-and-spoke).
- **Unique, useful content** per page. Thin or duplicate pages should be merged, expanded, or noindexed.

### Phase 5: Search intent and content strategy
- Map each target query to an intent: **informational, commercial investigation, transactional, navigational, local**.
- One primary intent per page. Don't make one page chase five unrelated queries.
- Build **topic clusters**: one comprehensive pillar page plus supporting pages, interlinked.
- Prefer original value: first-hand experience, case studies, data, screenshots, named authors, dates, and sources. This supports E-E-A-T (experience, expertise, authoritativeness, trust).
- Refresh important pages with real updates and visible "last updated" dates. Don't change dates without changing content.

### Phase 6: Structured data (schema.org JSON-LD)
Use only markup that matches visible page content. Validate with Google's Rich Results Test and Schema Markup Validator.

| Page type | Schema |
|---|---|
| Site-wide | `Organization` (name, url, logo, `sameAs` social/profile links, contactPoint) and `WebSite` |
| Local business | `LocalBusiness` (address, hours, geo, phone) |
| Product / shop | `Product` with `offers` (price, currency, availability); `AggregateRating` only with real, visible reviews |
| Articles / blog | `Article` or `BlogPosting` (headline, author, datePublished, dateModified, image) |
| Portfolio / projects | `CreativeWork`, `VideoObject`, `SoftwareApplication`, or `ImageObject` as appropriate |
| Video | `VideoObject` (name, description, thumbnailUrl, uploadDate); consider a video sitemap for self-hosted video |
| Navigation | `BreadcrumbList` |
| Q&A content | `FAQPage` only where a real FAQ is visible. Note: Google now shows FAQ rich results only for a narrow set of sites, but the markup still helps machines parse the content |

Also: `Person` for authors with `sameAs`, to establish entity identity. Don't mark up content that isn't on the page.

### Phase 7: AEO (answer engine optimization)
Goal: be the extractable answer.

- **Lead with the answer.** Put a 40-60 word direct answer immediately under the question-style heading, then elaborate.
- Use **question-based headings** that mirror real queries ("How much does X cost in {region}?", "What is Y?").
- Use **lists for steps/options**, **tables for comparisons**, **short definitions** for "what is" queries. Keep them as real HTML elements (`<ol>`, `<ul>`, `<table>`).
- Cover **follow-up questions** in the same page (the "People also ask" pattern).
- Write conversationally for **voice and long-tail queries**; include location and context where relevant.
- Keep key facts (price, hours, specs, definitions) in **plain text**, not only in images, PDFs, or JS widgets.
- For local intent: keep Google Business Profile complete and consistent with on-site name, address, phone (NAP). Check the primary category, hours, services, photos, and that reviews are answered; link the profile from the site and the site from the profile.

### Phase 8: GEO (generative engine optimization)
Goal: be retrievable, quotable, and clearly attributed in AI answers.

**Access**
- Decide deliberately which AI crawlers to allow in robots.txt. Common user agents: `GPTBot`, `OAI-SearchBot`, `ChatGPT-User` (OpenAI); `ClaudeBot`, `Claude-SearchBot`, `Claude-User` (Anthropic); `PerplexityBot`, `Perplexity-User`; `Google-Extended` (a control token for Gemini training, not a separate crawler); `Applebot-Extended`; `CCBot` (Common Crawl). Blocking training bots and allowing search/retrieval bots is a common middle path. Confirm current names in each vendor's documentation.
- AI crawlers generally do **not** execute JavaScript well, so server-rendered HTML matters even more for GEO than for Google.

**Content that gets cited**
- **Self-contained passages:** each section should make sense if extracted alone. Name the subject explicitly instead of "it" or "this".
- **Specific, verifiable facts:** numbers, dates, prices, named clients, named methods, with sources. Vague marketing language is rarely quoted.
- **Original data and firsthand material:** benchmarks, case studies, surveys, and unique explanations are what models and retrieval systems prefer to cite.
- **Clear entity definition:** one consistent brand name, a plain-language "what we are / who we serve / where" statement on the homepage and About page, consistent across the site, social profiles, directories, and `Organization` schema.
- **Authorship and trust signals:** named authors with bios, contact details, real addresses, policies, and citations to reputable sources.
- **Third-party corroboration:** AI systems weigh what others say about you. Pursue reviews, directory listings, press, partner pages, Wikipedia/Wikidata where notability genuinely applies, and relevant community discussions (done honestly, never astroturfed).
- **Freshness:** visible updated dates and current facts. Stale pricing or discontinued products get cited wrongly.

**`llms.txt` (optional, low-cost)**
- A markdown file at `/llms.txt` summarizing the site and linking key pages.
- **Status: proposed convention; major AI providers have not confirmed they use it for ranking or citation.** Treat as harmless, not as a lever.
- Keep it factual: company summary, services, key URLs, contact. Avoid internal details (admin paths, stack secrets, unreleased products).
- Keep it in sync with the real site; don't list pages that don't exist.

**Measure GEO manually.** There's no official dashboard. Run a fixed set of 15-30 buyer-style prompts monthly across ChatGPT, Claude, Perplexity, Gemini and Google AI Overviews; record whether the brand is mentioned, cited with a link, described accurately, and which competitors appear. Track referral traffic from AI domains in analytics.

### Phase 9: Authority and off-page
- Earn links through useful assets: tools, templates, research, case studies, guest expertise, partnerships.
- Fix brand-name inconsistency across domain, titles, social handles, and profiles.
- Claim and complete relevant profiles (Google Business Profile, Bing Places, LinkedIn, industry directories, app stores, GitHub).
- Don't buy links or use link networks.

### Phase 10: Measurement and iteration
- Set up Google Search Console and Bing Webmaster Tools; submit the sitemap; monitor the Pages (indexing) report, Performance, and Core Web Vitals.
- Track: indexed pages, impressions, clicks, CTR, average position by query group, conversions, AI referral traffic.
- Re-audit quarterly; refresh top pages; prune or merge low-value pages.

## Output format for audits

**Scale to the request.** For a quick audit (the user asked "check my site" or gave one page), cover Phases 2 and 4 on the pages provided and return: a 3-sentence summary, a findings table limited to the top 5-8 issues, and a short checkbox list. Use the full structure below only when the user asks for a full or site-wide audit.

Full audit: produce, in this order:

1. **Summary** (3-5 sentences): overall state and the single biggest blocker.
2. **What was checked and how** (files, tools, pages) plus **what could not be checked**.
3. **Findings table**: `Issue | Evidence | Impact (Critical/High/Medium/Low) | Fix`.
4. **Prioritized to-do list** with checkboxes, grouped Critical / High / Medium / Low.
5. **Quick wins** (under 1 hour each).
6. **Measurement plan.**

Keep recommendations concrete (give the rewritten title, the schema block, the sitemap entry), not generic advice.

## Prompt library

Ready-to-use prompts live in [prompts.md](prompts.md). Load it when the user wants a prompt for audits, keyword/intent mapping, on-page copy, schema, AEO/GEO rewrites, AI-visibility testing, llms.txt, or reporting. Replace the `{placeholders}` before use.

## Common mistakes to avoid

- Optimizing titles and keywords on pages that are not indexed or render blank.
- Splitting the brand across inconsistent names (e.g. domain says one thing, titles another).
- Sitemaps that omit deep pages, or that carry no `lastmod`.
- Schema that describes things not visible on the page.
- Treating GEO as a trick instead of clear, sourced, well-structured content.
- Blocking all AI crawlers and then expecting AI visibility (or the reverse, without a deliberate policy).
- Publishing mass AI-generated filler with no original value.
- Reporting rankings or traffic numbers that weren't measured.
