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

The skill scales to the request. It runs a short quick audit for a single page or a general "check my site", and the full six-part audit only when you ask for a full or site-wide one. Copy-only, schema-only and strategy requests skip the audit. Phase 2 includes curl checks (raw HTML, status and redirects, soft 404s, robots.txt, sitemap, canonical and robots meta), so it can verify a live site rather than reason about it.

## Install

Each tool reads skills from a folder containing `SKILL.md`. Copy the whole `seo-geo-aeo` folder (both files) into the location for your tool. The skill's `name` matches the folder name, which Gemini CLI and Cursor expect.

### Shared location (works in several tools)

`.agents/skills/` is read by Codex, Gemini CLI and Cursor, so it is the most portable choice:

```bash
# Per project (commit it so your team gets it)
mkdir -p .agents/skills
cp -r seo-geo-aeo .agents/skills/

# Or personal, for all your projects
mkdir -p ~/.agents/skills
cp -r seo-geo-aeo ~/.agents/skills/
```

### Per-tool details

| Tool | Project path | Personal path | Invoke |
|---|---|---|---|
| **Claude Code** | `.claude/skills/seo-geo-aeo/` | `~/.claude/skills/seo-geo-aeo/` | Automatic, or `/seo-geo-aeo` |
| **OpenAI Codex** | `.agents/skills/seo-geo-aeo/` | `~/.agents/skills/seo-geo-aeo/` | Automatic, `$seo-geo-aeo`, or `/skills` |
| **Gemini CLI** | `.gemini/skills/` or `.agents/skills/` | `~/.gemini/skills/` or `~/.agents/skills/` | Automatic; run `/skills` to confirm it loaded |
| **Cursor** | `.cursor/skills/` or `.agents/skills/` | `~/.cursor/skills/` or `~/.agents/skills/` | Automatic, or type `/` in Agent chat and search for it |

**Claude Code:** the folder is picked up live. If you create the top-level `skills` folder mid-session, run `/reload-skills`.

**OpenAI Codex:** new and changed skills are detected automatically. If it does not appear, restart Codex. To switch it off without deleting it, add this to `~/.codex/config.toml` and restart:

```toml
[[skills.config]]
path = "/path/to/seo-geo-aeo/SKILL.md"
enabled = false
```

**Gemini CLI:** you can install straight from this repository, or link a local copy while testing:

```bash
gemini skills install https://github.com/Mukiria/seo-geo-aeo
gemini skills link .      # run inside the skill folder
```

Start a new session afterwards. If the repository holds the skill at the root rather than in a `seo-geo-aeo/` folder, check the result with `/skills`, and copy it into a folder named `seo-geo-aeo` manually if it does not appear.

**Cursor:** copying the folder into one of the paths above is enough for local use. Cursor's GitHub import is for plugins, not bare skills: it expects a `.cursor-plugin/marketplace.json` in the repository, so importing this repo from GitHub will not work as-is.

**claude.ai:** zip the `seo-geo-aeo` folder and upload it as a skill in your account's skill settings.

Paths and commands come from each vendor's documentation and may change. Check your tool's current docs if something does not load.

## Use

The skill loads automatically when a request matches its description. You can also invoke it by name using your tool's syntax from the table above.

Example requests:

- "Audit https://example.com for SEO and AI-search visibility. Here are its robots.txt and sitemap."
- "Write title tags and meta descriptions for my services pages."
- "Generate Organization and Product JSON-LD from these details."
- "Create 25 prompts I can run in ChatGPT, Claude and Perplexity to test whether my brand gets cited."

## Notes and limitations

- **No guarantees.** The skill improves clarity and eligibility. It cannot promise rankings or AI citations.
- **`llms.txt` is optional and unproven.** It is a proposed convention, and major AI providers have not confirmed they use it for ranking or citation.
- **Verify crawler names.** AI crawler user-agent names in the GEO section can change. Confirm them in each vendor's documentation before editing `robots.txt`.
- **Measured data needed.** Rankings, traffic and Core Web Vitals must come from real tools (Search Console, PageSpeed Insights, a crawler such as Screaming Frog). The skill is written not to invent them.
- **Compatibility varies.** Loading behavior and slash-command support differ between tools, so test it in yours.

## Contributing

Issues and pull requests are welcome. Keep `SKILL.md` focused and under about 500 lines, and put long reference material in separate files such as `prompts.md`.

## License

Released under the [MIT License](LICENSE).
