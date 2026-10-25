# seo-geo-aeo

An Agent Skill for auditing and improving a website's visibility in three places:

- **SEO:** ranking in classic search results (Google, Bing).
- **AEO (Answer Engine Optimization):** featured snippets, "People also ask" and voice answers.
- **GEO (Generative Engine Optimization):** being mentioned and cited in AI-generated answers.

It gives an AI coding assistant a repeatable workflow (crawlability, on-page, structured data, AEO, GEO, measurement), an audit report format, and a library of ready-to-use prompts.

## What's inside

| File | Purpose |
|---|---|
| `SKILL.md` | The skill: ground rules, 10-phase workflow, audit output format, common mistakes |
| `prompts.md` | Prompt library for audits, keyword and intent mapping, on-page copy, schema, AEO/GEO rewrites, AI-visibility testing, `llms.txt` and reporting |

`SKILL.md` loads `prompts.md` only when it is needed, which keeps the main file short.

The skill scales to the request. It runs a short quick audit for a single page or a general "check my site", and the full six-part audit only when you ask for a full or site-wide one. Copy-only, schema-only and strategy requests skip the audit. Phase 2 includes `curl` checks (raw HTML, status and redirects, soft 404s, `robots.txt`, sitemap, canonical and robots meta), so it can verify a live site rather than reason about it.

## Install

Copy the `seo-geo-aeo` folder (containing both files) into a skills directory.

**Any tool that supports the Agent Skills format** (recommended for portability):

```bash
# Per project
mkdir -p .agents/skills
cp -r seo-geo-aeo .agents/skills/

# Or for all your projects
mkdir -p ~/.agents/skills
cp -r seo-geo-aeo ~/.agents/skills/
```

**Claude Code:**

```bash
# Per project
mkdir -p .claude/skills && cp -r seo-geo-aeo .claude/skills/

# Or personal (all projects on this machine)
mkdir -p ~/.claude/skills && cp -r seo-geo-aeo ~/.claude/skills/
```

**claude.ai:** zip the `seo-geo-aeo` folder and upload it as a skill in your account's skill settings.

Other tools that read the same format may use their own folders (for example `.github/skills/`, `.gemini/skills/` or `.cursor/skills/`). Check your tool's documentation.

## Use

The skill loads automatically when a request matches its description. In tools that support slash commands, you can also invoke it directly:

```
/seo-geo-aeo
```

Example requests:

- "Audit https://example.com for SEO and AI-search visibility. Here are its robots.txt and sitemap."
- "Quick-check this page for SEO issues: https://example.com/services"
- "Write title tags and meta descriptions for my services pages."
- "Generate Organization and Product JSON-LD from these details."
- "Create 25 prompts I can run in ChatGPT, Claude and Perplexity to test whether my brand gets cited."

## Notes and limitations

- **No guarantees.** The skill improves clarity and eligibility. It cannot promise rankings or AI citations.
- **`llms.txt` is optional and unproven.** It is a proposed convention, and major AI providers have not confirmed they use it for ranking or citation.
- **Verify time-sensitive claims.** AI crawler user-agent names, which rich results Google still shows (such as FAQ), whether AI crawlers run JavaScript, and the status of `llms.txt` can all change. The skill was last reviewed on 2026-10-25 from its text alone, not against vendor documentation. Confirm these in each vendor's current documentation before acting on them, for example before editing `robots.txt`.
- **Measured data needed.** Rankings, traffic and Core Web Vitals must come from real tools (Search Console, PageSpeed Insights, a crawler such as Screaming Frog). The skill is written not to invent them.
- **Compatibility varies.** Loading behavior and slash-command support differ between tools, so test it in yours.

## Contributing

Issues and pull requests are welcome. Keep `SKILL.md` focused and under about 500 lines, and put long reference material in separate files such as `prompts.md`.

## License

Released under the [MIT License](LICENSE).
