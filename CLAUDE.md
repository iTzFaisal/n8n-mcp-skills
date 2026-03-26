# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Purpose

This is a **knowledge repository**, not a traditional code project. It contains curated documentation (skills) that enable AI agents to assist users in building n8n workflows. The repository has no build system, tests, or compilation steps.

## Architecture

### Dual Platform Skills

Skills are mirrored for two platforms:

- `.claude/skills/` — Claude Code / Cloud Code
- `.agents/skills/` — OpenCode Plugin

Both locations contain identical skill content. Skills are sourced from `czlonkowski/n8n-skills` (tracked in `skills-lock.json`).

### The 7 Core Skills

1. **n8n-code-javascript** — JavaScript in Code nodes (`$input`, `$json`, `$helpers`, HTTP requests, DateTime)
2. **n8n-code-python** — Python in Code nodes (`_input`, `_json`, `_node`, standard library)
3. **n8n-expression-syntax** — n8n `{{ }}` expression language validation
4. **n8n-mcp-tools-expert** — MCP tool usage guide (node discovery, validation, workflow management)
5. **n8n-node-configuration** — Operation-aware node configuration guidance
6. **n8n-validation-expert** — Interpreting validation errors and fixing workflows
7. **n8n-workflow-patterns** — Architectural patterns (webhook, HTTP API, database, AI agents, scheduled)

### MCP Configuration

- `.mcp.json` — For Claude Code / Cloud Code (MCP stdio mode)
- `opencode.json` — For OpenCode environments

Both require `N8N_API_URL` and `N8N_API_KEY` environment variables. Example files provided as `.mcp.json.example` and `opencode.json.example`.

## Key Concepts

### nodeType Format Differences

**Critical**: Tools use different nodeType formats:

| Tool Type         | Format             | Example                |
| ----------------- | ------------------ | ---------------------- |
| Search/Validate   | `nodes-base.*`     | `nodes-base.slack`     |
| Workflow creation | `n8n-nodes-base.*` | `n8n-nodes-base.slack` |

Use the format returned by `search_nodes` — it provides both formats.

### Skill Interconnections

Skills cross-reference each other:

- Workflow patterns reference node configuration and validation skills
- MCP tools expert references all other skills for tool selection
- Code skills reference expression syntax for data access

### Validation Profiles

The n8n-mcp validation supports multiple profiles:

- `minimal` — Required fields only (fast, permissive)
- `runtime` — Values + types (default, recommended)
- `ai-friendly` — Reduced false positives
- `strict` — Maximum validation (production)

## Common Tasks

### Adding a New Skill

1. Create skill directory in both `.claude/skills/` and `.agents/skills/`
2. Add `SKILL.md` with frontmatter (name, description)
3. Update `skills-lock.json` with source tracking
4. Ensure content is identical in both locations

### Updating MCP Configuration

Edit `.mcp.json` or `opencode.json` with credentials:

```json
{
  "N8N_API_URL": "http://localhost:5678",
  "N8N_API_KEY": "your-api-key-here"
}
```

Note: Actual credentials are in `.gitignore` - only commit the `.example` files.

### Validating Skill Structure

```bash
# Verify skill count
find .claude/skills -name "SKILL.md" | wc -l  # Should be 7

# Count documentation files
find . -name "*.md" | grep -v node_modules | wc -l
```

## Repository Stats

- 7 core skills (14 implementations total - dual platform)
- ~72 documentation files (~44,000 lines)
- 40+ MCP tools available via n8n-mcp
- 2,700+ n8n templates accessible
- 2,000+ nodes searchable

## External References

- n8n documentation: https://docs.n8n.io/
- n8n MCP server: https://github.com/czlonkowski/n8n-mcp
- Original skills: https://github.com/czlonkowski/n8n-skills
