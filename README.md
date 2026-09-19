# PyreCrawl Skills

Downloadable workflow skills for AI agents using [PyreCrawl](https://github.com/SanggonBoy/PyreCrawl) MCP tools.

## What are skills?

Skills are instruction files that tell your AI agent **how** to use PyreCrawl tools effectively — research protocols, anti-hallucination workflows, tool routing rules, and best practices.

Drop a skill into your project and your agent reads it automatically.

## Installation

### Claude Code
```bash
# Clone the skill you need into your project
git clone https://github.com/SanggonBoy/pyrecrawl-skills.git /tmp/pyrecrawl-skills
cp -r /tmp/pyrecrawl-skills/pyrecrawl-research/SKILL.md ./CLAUDE.md
```

### Cursor
```bash
git clone https://github.com/SanggonBoy/pyrecrawl-skills.git /tmp/pyrecrawl-skills
cp /tmp/pyrecrawl-skills/pyrecrawl-research/SKILL.md .cursorrules
```

### Codex / OpenCode
```bash
git clone https://github.com/SanggonBoy/pyrecrawl-skills.git /tmp/pyrecrawl-skills
cp /tmp/pyrecrawl-skills/pyrecrawl-research/SKILL.md ./AGENTS.md
```

### Any Agent
Copy the contents of any `SKILL.md` into your agent's instruction file (CLAUDE.md, .cursorrules, AGENTS.md, etc.)

## Available Skills

| Skill | Description |
|-------|-------------|
| [pyrecrawl-research](pyrecrawl-research/) | Multi-step research workflow with anti-hallucination protocol |

## Prerequisites

- [PyreCrawl](https://github.com/SanggonBoy/PyreCrawl) MCP server installed and configured
- An AI agent that supports MCP tools (Claude Code, Cursor, Codex, OpenCode, Hermes, etc.)

## License

MIT
