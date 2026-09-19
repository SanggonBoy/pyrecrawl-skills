# PyreCrawl Research Skill

You have access to PyreCrawl MCP tools for web scraping, crawling, and research. This skill tells you HOW to use those tools effectively. Follow this protocol for ALL research tasks.

## When to Use This Skill

- User asks to research, investigate, or deep-dive into a topic
- User shares URLs to analyze or compare
- User asks fact-checking questions
- User needs competitive intelligence or market research
- User asks "what is X", "tell me about X", "compare X and Y"
- User says "I want to build X like Y" (requires reference analysis)

## Tool Routing

| User Intent | Tool to Use | Why |
|-------------|-------------|-----|
| Simple search | `web_search` (built-in) | Fast, no anti-bot needed |
| Search with Cloudflare bypass | `pyrecrawl_search` | DDG bot detection bypass |
| Read/scrape a URL | `pyrecrawl_scrape` | Auto-escalates past blocks |
| Research a topic | `pyrecrawl_deep_research` | Search + scrape + citations |
| Scrape multiple URLs | `pyrecrawl_batch_scrape` | Parallel, deduped |
| Extract structured data | `pyrecrawl_extract` | CSS schema → JSON |
| Crawl entire site | `pyrecrawl_crawl` | Multi-page discovery |
| Academic papers | `pyrecrawl_search_papers` | arXiv / Crossref |
| Read PDF/DOCX | `pyrecrawl_document` | Document extraction |
| Monitor page changes | `pyrecrawl_monitor` | Baseline + diff |
| Login-walled pages | `pyrecrawl_session` | Persistent browser |

**Never** use `web_extract` (built-in) for JS-heavy or Cloudflare-protected sites — use `pyrecrawl_scrape` instead.

## Research Protocol

### Phase 1: Local Context (if applicable)

Before fetching from the internet, check if local context exists:

```
1. If user has a project/codebase → read relevant files first (search_files, read_file)
2. If user shared a URL → pyrecrawl_scrape(url) first to understand the reference
3. Build a mental model of what the user already has before searching for what they need
```

### Phase 2: Research Gathering

#### Standard Research (1-2 passes)

```
1. pyrecrawl_deep_research(query="topic", limit=5, scrape_top=3, iterations=1)
2. Read ALL evidence carefully
3. Go to Phase 3: Gap Analysis
```

#### Deep Research (2-3 passes, for complex topics)

```
1. pyrecrawl_deep_research(query="topic", limit=5, scrape_top=3, iterations=3)
2. Read ALL evidence across all passes
3. Go to Phase 3: Gap Analysis
```

### Phase 3: Gap Analysis (MANDATORY — do not skip)

After each research pass, answer these questions BEFORE synthesizing:

```
□ Do I have information from at least 3 independent sources?
□ Are there aspects of the topic I haven't covered?
□ Do any sources conflict? Have I noted both sides?
□ Am I missing recent information (last 6 months)?
□ Am I missing academic/authoritative sources?
□ Do I have enough to give a confident answer, or am I guessing?
```

**Decision:**
- If ALL boxes checked → proceed to Phase 4 (Synthesis)
- If ANY box unchecked → go back to Phase 2 with a targeted query:
  - Missing aspects → `pyrecrawl_deep_research(query="topic specific missing aspect")`
  - Missing recency → `pyrecrawl_deep_research(query="topic latest developments 2025")`
  - Missing academic → `pyrecrawl_search_papers(query="topic", source="arxiv")`
  - Conflicting sources → `pyrecrawl_deep_research(query="topic vs comparison")`
- **MAX 3 total research iterations** — after that, synthesize with what you have and note gaps

### Phase 4: Synthesis (MANDATORY format)

Present results using this exact structure:

```markdown
## [Topic]

**Research depth:** [standard/deep] | **Sources:** [N] | **Confidence:** [high/medium/low]

### Key Findings
- Finding 1 [1]
- Finding 2 [2]
- Finding 3 [3]

### Details
[Detailed explanation with inline [n] citations for EVERY factual claim]

### Conflicting Views
- Source A says X [3], but Source B says Y [4]
- [Explain why they might differ]

### Unknowns
- [What you could NOT find evidence for]
- [What would need deeper investigation]

### Sources
[1] Title - URL
[2] Title - URL
[3] Title - URL
```

**NEVER skip the Unknowns section.** If you don't know something, say so.

## Anti-Hallucination Rules (HARD — no exceptions)

1. **Every factual claim must have a [n] citation** from the evidence pack
2. **Never fabricate URLs** — only cite URLs that appear in tool results
3. **Never fabricate statistics** — if a number isn't in the evidence, say "exact figure not found in sources"
4. **Conflicting sources** — state both sides, don't pick one silently
5. **Insufficient evidence** — say "based on available sources" and list what was searched
6. **"I don't know" is a valid answer** — better than guessing

## Error Recovery

| Error | Action |
|-------|--------|
| `pyrecrawl_scrape` blocked | Retry with `prefer="stealth"` |
| `pyrecrawl_search` no results | Try `pyrecrawl_deep_research` instead |
| `pyrecrawl_deep_research` timeout | Reduce `scrape_top` to 2, retry |
| `pyrecrawl_session` login fail | Use `action="open"` first, then `action="fill"` |
| All engines fail | Report honestly: "unable to access this source" |
| `pyrecrawl_extract` schema error | Run `pyrecrawl_scrape` first to see raw markdown, fix selectors |

## Anti-Patterns (DO NOT)

- ❌ Scraping a URL when `web_extract` would suffice (waste of resources)
- ❌ Using `pyrecrawl_crawl` for a single page (use `pyrecrawl_scrape`)
- ❌ Running `pyrecrawl_deep_research` for simple factual lookups (use `web_search`)
- ❌ Claiming "I researched this" without calling any tools
- ❌ Synthesizing from only 1 source — always aim for 3+ sources minimum
- ❌ Ignoring `iterations` parameter — use `iterations=2-3` for complex topics
- ❌ Skipping Gap Analysis (Phase 3) — always check before answering
- ❌ Skipping Unknowns section — always state what you couldn't find
- ❌ Giving a confident answer with low-confidence evidence
