# PyreCrawl Skills

Downloadable workflow skills for AI agents using [PyreCrawl](https://github.com/SanggonBoy/PyreCrawl) MCP tools.

## What are skills?

PyreCrawl MCP tools give your agent **hands** — the ability to scrape, crawl, search, and extract from the web.

Skills give your agent a **brain** — instructions on *when* to use which tool, *how* to chain research passes, and *what* anti-hallucination rules to follow.

| | [PyreCrawl MCP Tools](https://github.com/SanggonBoy/PyreCrawl) | PyreCrawl Skills (this repo) |
|---|---|---|
| **Role** | Execute web operations | Tell the agent how to use them |
| **Analogy** | Hands | Brain |
| **Example** | `deep_research(query, iterations=3)` | "Run 3 passes, check gaps after each, cite everything" |
| **Required?** | Yes (the engine) | Optional (but recommended for research quality) |

> **Without skills:** Your agent has powerful tools but improvises usage.
> **With skills:** Your agent follows a proven research protocol with anti-hallucination guardrails.

## Installation

### Step 1: Install PyreCrawl MCP Tools (required)

```bash
uvx pyrecrawl@latest
```

Or see [PyreCrawl README](https://github.com/SanggonBoy/PyreCrawl#-installation) for full instructions.

### Step 2: Add a Skill to Your Project

Copy the skill's `SKILL.md` into your agent's instruction file:

**Claude Code:**
```bash
git clone https://github.com/SanggonBoy/pyrecrawl-skills.git /tmp/pyrecrawl-skills
cp /tmp/pyrecrawl-skills/pyrecrawl-research/SKILL.md ./CLAUDE.md
```

**Cursor:**
```bash
git clone https://github.com/SanggonBoy/pyrecrawl-skills.git /tmp/pyrecrawl-skills
cp /tmp/pyrecrawl-skills/pyrecrawl-research/SKILL.md .cursorrules
```

**Codex / OpenCode:**
```bash
git clone https://github.com/SanggonBoy/pyrecrawl-skills.git /tmp/pyrecrawl-skills
cp /tmp/pyrecrawl-skills/pyrecrawl-research/SKILL.md ./AGENTS.md
```

**Any Agent:** Copy the contents of any `SKILL.md` into your agent's instruction file.

## Available Skills

| Skill | Description |
|-------|-------------|
| [pyrecrawl-research](pyrecrawl-research/) | Multi-step research workflow with gap analysis, anti-hallucination protocol, and mandatory citation rules |

## Prerequisites

- [PyreCrawl](https://github.com/SanggonBoy/PyreCrawl) MCP server installed and configured
- An AI agent that supports MCP tools (Claude Code, Cursor, Codex, OpenCode, Hermes, etc.)

## License

MIT
