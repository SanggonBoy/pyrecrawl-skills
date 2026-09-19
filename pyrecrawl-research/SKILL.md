# PyreCrawl Research Skill

You have access to PyreCrawl MCP tools for web scraping, crawling, and research. Follow this protocol for ALL research tasks to ensure grounded, citation-backed responses.

## When to Use This Skill

- User asks to research, investigate, or deep-dive into a topic
- User shares URLs to analyze or compare
- User asks fact-checking questions
- User needs competitive intelligence or market research
- User asks "what is X", "tell me about X", "compare X and Y"

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

### Standard Research (1-2 passes)

```
1. pyrecrawl_deep_research(query="topic", limit=5, scrape_top=3, iterations=1)
2. Read all evidence carefully
3. Synthesize answer with [n] citations for every claim
4. If gaps remain → go to Deep Research
```

### Deep Research (2-3 passes, for complex topics)

```
1. pyrecrawl_deep_research(query="topic", limit=5, scrape_top=3, iterations=3)
2. Read ALL evidence across all passes
3. Identify conflicting sources → state the disagreement
4. Identify unsupported claims → mark "needs source"
5. If critical gaps remain:
   a. pyrecrawl_deep_research(query="topic specific aspect", iterations=2)
   b. pyrecrawl_search_papers(query="topic", source="arxiv") for academic backing
6. Final synthesis with citations
```

### URL Analysis

```
1. pyrecrawl_scrape(url="...", prefer="auto")
2. Analyze the markdown content
3. If more context needed → pyrecrawl_deep_research(query="related topic")
4. Cross-reference scraped content with search results
```

## Anti-Hallucination Rules

1. **Every factual claim must have a [n] citation** from the evidence pack
2. **Never fabricate URLs** — only cite URLs that appear in tool results
3. **Never fabricate statistics** — if a number isn't in the evidence, say "exact figure not found in sources"
4. **Conflicting sources** — state both sides, don't pick one silently
5. **Insufficient evidence** — say "based on available sources" and list what was searched
6. **After each research pass**, explicitly check: "What do I still NOT know?" before answering

## Evidence Synthesis Template

When presenting research results, use this structure:

```
## [Topic]

### Key Findings
- Finding 1 [1]
- Finding 2 [2]

### Details
[Detailed explanation with inline citations]

### Conflicting Views
- Source A says X [3], but Source B says Y [4]

### Sources
[1] Title - URL
[2] Title - URL
...
```

## Error Recovery

| Error | Action |
|-------|--------|
| `pyrecrawl_scrape` blocked | Retry with `prefer="stealth"` |
| `pyrecrawl_search` no results | Try `pyrecrawl_deep_research` instead |
| `pyrecrawl_deep_research` timeout | Reduce `scrape_top` to 2, retry |
| `pyrecrawl_session` login fail | Use `action="open"` first, then `action="fill"` |
| All engines fail | Report honestly: "unable to access this source" |

## Anti-Patterns (DO NOT)

- ❌ Scraping a URL when `web_extract` would suffice (waste of resources)
- ❌ Using `pyrecrawl_crawl` for a single page (use `pyrecrawl_scrape`)
- ❌ Running `pyrecrawl_deep_research` for simple factual lookups (use `web_search`)
- ❌ Claiming "I researched this" without calling any tools
- ❌ Synthesizing from only 1 source — always aim for 3+ sources minimum
- ❌ Ignoring `iterations` parameter — use `iterations=2-3` for complex topics
