# pyrecrawl-research

Research workflow skill for AI agents using PyreCrawl MCP tools.

## What it does

Tells your AI agent how to:
- Route tool selection (which tool for which task)
- Run multi-step research with evidence gathering
- Ground every claim in cited sources
- Avoid hallucination by following the anti-hallucination protocol
- Recover from tool errors gracefully

## Installation

Copy `SKILL.md` to your agent's instruction file:

```bash
# Claude Code
cp SKILL.md /path/to/your/project/CLAUDE.md

# Cursor
cp SKILL.md /path/to/your/project/.cursorrules

# Codex / OpenCode
cp SKILL.md /path/to/your/project/AGENTS.md
```

Or merge its contents into your existing instruction file.

## Prerequisites

- [PyreCrawl](https://github.com/SanggonBoy/PyreCrawl) MCP server installed
- An AI agent with MCP tool support

## License

MIT
