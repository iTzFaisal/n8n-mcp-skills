# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Purpose

This is an **OpenCode plugin repository** for n8n-mcp integration. It provides specialized skills and agents for working with n8n workflows through MCP (Model Context Protocol) tools. The project is entirely documentation-driven with no traditional source code.

## Project Structure

```
.opencode/
├── agents/
│   └── n8n.md                    # Main n8n workflow expert agent
├── skills/
│   ├── n8n-code-javascript/      # JavaScript Code node expertise
│   ├── n8n-code-python/          # Python Code node guidance
│   ├── n8n-expression-syntax/    # n8n expression language mastery
│   ├── n8n-mcp-tools-expert/     # MCP tool usage specialist
│   ├── n8n-node-configuration/   # Node configuration patterns
│   ├── n8n-validation-expert/    # Validation workflows expert
│   └── n8n-workflow-patterns/    # Workflow architecture patterns
└── package.json                  # OpenCode plugin dependency

opencode.json                      # MCP server configuration
.mcp.json                          # MCP client configuration
AGENTS.md                          # Complete documentation standards
```

## Validation Commands

This repository has no traditional build system (no package.json, tsconfig.json, or test suites). Use these commands to validate content:

```bash
# Validate JSON configuration
cat opencode.json | jq .

# Check file structure (should find 7 skills and 1+ agents)
find .opencode/skills -name "SKILL.md" | wc -l
find .opencode/agents -name "*.md" | wc -l

# Verify frontmatter in skills
head -5 .opencode/skills/*/SKILL.md | grep "^name:"

# Verify frontmatter in agents
head -20 .opencode/agents/*.md | grep "^description:"

# Validate Markdown syntax (if markdownlint is installed)
markdownlint .opencode/**/*.md
```

## MCP Server Configuration

The project configures n8n as an MCP server in `opencode.json`:
- **Type**: Local process execution via `npx n8n-mcp`
- **Mode**: stdio communication
- **Environment**: Requires `N8N_API_URL` and `N8N_API_KEY`
- **Settings**: Error logging enabled, console output disabled

## Documentation Standards

### Frontmatter Requirements

**Skills** (YAML at top of SKILL.md):
```yaml
---
name: skill-identifier-kebab-case
description: One-line description. Use when [triggers]. Provides [value].
---
```

**Agents** (YAML at top of agent .md file):
```yaml
---
description: >-
  Multi-line description explaining when to use this agent.

  <example>
  Context: Situation description
  User: "User request"
  Assistant: "Agent response"
  </example>
mode: all
color: "#ff0000"
---
```

### Content Patterns

Every skill must include:
1. **Quick Start/Quick Reference** - First practical section
2. **Error Prevention** - Common mistakes with ❌/✅ examples
3. **Best Practices** - Production-tested recommendations
4. **Integration Section** - How this skill relates to others

### Markdown Conventions

- **Sections**: `## Main Section` → `### Subsection` → `#### Sub-subsection`
- **Code blocks**: Always specify language (` ```javascript `, ` ```json `, ` ```bash `)
- **Comparisons**: Use `// ❌ WRONG:` and `// ✅ CORRECT:` pattern
- **Horizontal rules**: Use `---` between major sections
- **Links**: Internal `[SKILL.md](SKILL.md)`, external `[n8n Docs](https://docs.n8n.io/)`

### Naming Conventions

- **Skills**: `n8n-domain-subdomain` (kebab-case)
- **Files**: `UPPERCASE.md` for key docs, `lowercase.md` for supporting files
- **Variables**: Use descriptive names (`activeUsers` not `a`)

## Architecture

### Skill System

The repository contains 7 specialized skills that cover different aspects of n8n development:

1. **n8n-code-javascript** - JavaScript code in Code nodes
2. **n8n-code-python** - Python code in Code nodes
3. **n8n-expression-syntax** - n8n expression language (`{{}}` syntax)
4. **n8n-mcp-tools-expert** - MCP tool usage patterns
5. **n8n-node-configuration** - Node configuration by operation
6. **n8n-validation-expert** - Workflow and node validation
7. **n8n-workflow-patterns** - Architectural patterns for workflows

Skills are cross-referenced and designed to work together. Each skill typically includes:
- `SKILL.md` (400-700 lines) - Main content
- `README.md` (250-350 lines) - Metadata and overview
- Supporting files (e.g., `ERROR_PATTERNS.md`, `COMMON_PATTERNS.md`)

### Agent Architecture

The n8n agent (`.opencode/agents/n8n.md`) follows these principles:
- **Silent Execution**: Tools run without commentary
- **Parallel Operations**: Independent calls executed in parallel
- **Templates First**: Check 2,709+ templates before building from scratch
- **Multi-Level Validation**: Use minimal → full → workflow validation pattern
- **Never Trust Defaults**: Always explicitly configure all parameters

## Testing

No traditional test suite. Testing is done through:
- OpenCode integration testing
- Skill activation testing with trigger keywords
- Cross-reference validation between skills
- Verification of frontmatter and markdown syntax

## Key Files

- **AGENTS.md**: Complete documentation standards for coding agents
- **opencode.json**: MCP server configuration for n8n API
- **.opencode/agents/n8n.md**: Main agent with workflow process (433 lines)
- **.opencode/skills/*/SKILL.md**: Individual skill implementations

## Important Context

- This is a **documentation-only repository** - no source code
- All content is in Markdown with YAML frontmatter
- Skills are designed for OpenCode AI integration
- MCP tools provide access to n8n API for workflow management
- Statistics from real usage are included when available (e.g., "38% of failures")
