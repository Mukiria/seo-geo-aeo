# SEO / GEO / AEO Prompt Library

Companion to [SKILL.md](SKILL.md). Replace `{placeholders}`. Paste data (HTML, crawl exports, Search Console exports) after the prompt where noted.

### Audit and diagnosis

**Full-site audit**
```
Act as a senior technical SEO. Audit {domain}. I've provided: {robots.txt / sitemap / homepage HTML / crawl export}.
For each finding give: evidence, impact (Critical/High/Medium/Low), and a specific fix.
Separate what you verified from what you're inferring. List what you could NOT check and which tool would check it.
Finish with a prioritized checkbox to-do list.
```

**Rendering check (JS sites)**
```
Here is the raw HTML response (view-source) and the rendered DOM for {URL}.
Compare them. Tell me which content, links, headings, and structured data exist only after JavaScript runs, and the risk this creates for Google and for AI crawlers.
Recommend SSR, static generation, or prerendering, with the smallest change for a {framework} app.
```

**Search Console triage**
```
Here is my Search Console Pages (indexing) report export. Group the excluded URLs by reason, explain what each reason means, tell me which are expected vs. problems, and give the fix for each problem group in priority order.
```

**Performance interpretation**
```
Here are my PageSpeed Insights / Lighthouse results for {URL}. Rank the issues by likely effect on LCP, INP and CLS, and give the specific code or config change for each of the top 5.
```

### Keywords, intent, strategy

**Query and intent map**
```
Business: {description}. Audience: {who, where}. Offer: {services/products}.
Generate 40 target queries grouped by intent (informational, commercial, transactional, local). For each, give the page type that should target it and whether it needs a new page or an existing one.
Don't invent search volumes; tell me how to validate them with {Search Console / Keyword Planner / Ahrefs}.
```

**Topic cluster**
```
Build a topic cluster around "{pillar topic}" for {audience}. Give: one pillar page outline, 8-12 supporting pages with target query and intent, and the internal linking plan between them.
```

**Competitor gap**
```
Compare my page {URL or pasted text} against these top-ranking pages: {URLs or pasted text}.
List the subtopics, questions, formats, and evidence they cover that I don't, and what original value I can add that they lack.
```

### On-page copy

**Title and meta**
```
Write 5 title tag options (max 60 chars) and 3 meta descriptions (max 155 chars) for a page about {topic}, target query "{query}", brand "{brand}". Match {search intent}. No clickbait, no keyword stuffing. Mark the recommended pair.
```

**Rewrite for AEO**
```
Rewrite this page section so it opens with a direct 40-60 word answer to "{question}", then expands. Use a question-style H2, add a list or table where it helps, and keep every claim specific and verifiable. Don't add facts I haven't provided; flag where I need to supply data.
```

**FAQ block**
```
From this page content, write 6-8 real customer questions with concise, accurate answers (2-4 sentences). Only use facts present in the content. Output visible HTML and matching FAQPage JSON-LD.
```

### Structured data

**Schema generator**
```
Generate valid JSON-LD for a {Organization / LocalBusiness / Product / Article / VideoObject / SoftwareApplication} using only the facts below. Don't invent ratings, reviews, prices or addresses. Mark any required field I haven't supplied.
Facts: {paste}
```

**Schema review**
```
Review this JSON-LD against the visible page content and schema.org / Google guidelines. List errors, missing recommended properties, and any markup that isn't supported by visible content.
```

### GEO and AEO

**Entity clarity audit**
```
Read my homepage and About page text. In 3 sentences, state who this company is, what it offers, for whom, and where, using only what the pages say.
Then list every ambiguity, inconsistency (names, spellings, claims) or missing fact that would make an AI system describe us wrongly or skip us.
```

**AI-citability rewrite**
```
Rewrite these paragraphs so each is self-contained and quotable: name the subject explicitly, state one specific fact with its source or date, remove filler. Don't change meaning or add claims. Show before/after.
```

**AI visibility test set**
```
Create 25 prompts a potential customer of {business} might ask an AI assistant, split into: discovery ("best {service} in {location}"), comparison ("{us} vs {competitor}"), problem-led ("how do I {problem}"), and brand ("what is {brand}"). I'll run them in ChatGPT, Claude, Perplexity and Gemini and record mentions, citations and accuracy.
```

**AI answer analysis (paste results)**
```
Here are AI-assistant answers to my test prompts. For each: Was {brand} mentioned? Cited with a link? Described accurately? Which competitors and which source domains appeared?
Then identify the 5 content or authority gaps most likely causing misses, and the page to create or fix for each.
```

**llms.txt draft**
```
Write an llms.txt for {domain}: H1 with the brand, a one-paragraph blockquote summary, then sections linking only to pages that exist, each with a one-line description. Include contact details. Exclude admin paths, internal tooling and anything unreleased. Use only the facts I provide.
```

### Authority and monitoring

**Outreach assets**
```
Suggest 10 link-worthy assets {brand} could genuinely create from its own expertise (data, tools, templates, case studies), with the type of site that would reference each. No paid or manipulative tactics.
```

**Monthly SEO report**
```
Using this Search Console and Analytics export for {period}, summarize: wins, losses, top queries gained/lost, pages with falling CTR, indexing changes, and AI-referral traffic. End with 5 prioritized actions for next month. Don't speculate beyond the data.
```
