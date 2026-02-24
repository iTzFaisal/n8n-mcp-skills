# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is an **n8n MCP (Model Context Protocol) Integration Repository** - a specialized documentation-driven project that provides Claude Code with comprehensive capabilities for working with n8n workflows through MCP tools. The repository contains no traditional source code but instead houses extensive skill and agent documentation for OpenCode integration.

## Key Architecture

### Documentation-Driven Skills Repository

This is not a traditional code repository. It's a **knowledge base** for AI-assisted n8n workflow development.

- **Skills**: 7 core skills mirrored in `.claude/skills/` and `.opencode/skills/`
- **Format**: Markdown with YAML frontmatter
- **Purpose**: Guide AI agents in using n8n MCP tools effectively
- **Total Content**: ~44,000 lines across 72 markdown files

### MCP Server Configuration

The n8n-mcp server provides tools for workflow automation:

```json
{
  "mcpServers": {
    "n8n-mcp": {
      "command": "npx",
      "args": ["n8n-mcp"],
      "env": {
        "MCP_MODE": "stdio",
        "N8N_API_URL": "http://localhost:5678",
        "N8N_API_KEY": "<your-api-key>"
      }
    }
  }
}
```

**Configuration Files**:

- `opencode.json` - OpenCode plugin configuration
- `.mcp.json` - MCP server configuration (same as above)
- `.opencode/package.json` - Plugin dependencies (`@opencode-ai/plugin`)

### Skills Architecture

The 7 core skills:

1. **n8n-code-javascript** - JavaScript in Code nodes
2. **n8n-code-python** - Python in Code nodes
3. **n8n-expression-syntax** - n8n expression language (`{{}}`)
4. **n8n-mcp-tools-expert** - MCP tool usage patterns
5. **n8n-node-configuration** - Node configuration patterns
6. **n8n-validation-expert** - Workflow validation
7. **n8n-workflow-patterns** - Architectural patterns

Each skill contains:

- `SKILL.md` - Main content (400-1100 lines)
- `README.md` - Metadata and overview
- Supporting files (ERROR_PATTERNS.md, COMMON_PATTERNS.md, etc.)

## Development and Validation

### No Build System

There is **no package.json at the root level**, no TypeScript compilation, and no test suites. This is a pure documentation repository.

### Validation Commands

```bash
# Validate JSON configuration
cat opencode.json | jq .

# Verify skill structure
find .claude/skills -name "SKILL.md" | wc -l  # Should be 7
find .opencode/skills -name "SKILL.md" | wc -l  # Should be 7

# Verify frontmatter in skills
head -5 .claude/skills/*/SKILL.md | grep "^name:"

# Count documentation
find . -name "*.md" | grep -v node_modules | wc -l  # 72 files
```

### Testing Approach

Skills are tested through:

1. OpenCode AI integration activation
2. Trigger keyword verification
3. Cross-reference link validation
4. Markdown syntax verification

## Architecture Patterns

### 1. Dual Storage Pattern

Skills exist in both `.claude/skills/` and `.opencode/skills/`:

- `.claude/skills/` - Claude Code access
- `.opencode/skills/` - OpenCode plugin access
- Both should remain synchronized

### 2. Cross-Referenced Knowledge Graph

Each skill has an "Integration with Other Skills" section linking to related capabilities, creating an interconnected knowledge system.

### 3. Progressive Documentation Structure

Skills follow this pattern:

- Quick Start → Detailed Examples → Common Errors → Best Practices → Integration
- Statistics included when available (e.g., "38% of failures")
- Production examples with real-world patterns

### 4. MCP Tool Categories

The n8n-mcp server provides 40+ tools in these categories:

1. **Node Discovery**: `search_nodes`, `get_node`, `validate_node`
2. **Workflow Management**: `n8n_create_workflow`, `n8n_update_partial_workflow`, `n8n_update_full_workflow`
3. **Template Library**: `search_templates`, `n8n_deploy_template` (2,700+ templates)
4. **Validation**: `validate_workflow`, `validate_node`
5. **Execution**: `n8n_test_workflow`, `n8n_executions`
6. **Documentation**: `tools_documentation`, `get_node` (mode="docs")

## Documentation Standards

### Frontmatter Format

**Skills** (YAML in SKILL.md):

```yaml
---
name: skill-identifier-kebab-case
description: One-line description. Use when [triggers]. Provides [value].
---
```

### Markdown Conventions

- **Sections**: `## Main Section` → `### Subsection` → `#### Sub-subsection`
- **Code blocks**: Always specify language (` ```javascript `, ` ```json `, ` ```bash `)
- **Error patterns**: Use ❌ WRONG / ✅ CORRECT format
- **Links**: `[SKILL.md](SKILL.md)` for internal, `[n8n Docs](https://docs.n8n.io/)` for external
- **Separators**: Use `---` between major sections

### Naming Conventions

- **Skills**: `n8n-domain-subdomain` (kebab-case)
- **Key files**: `SKILL.md`, `README.md`, `ERROR_PATTERNS.md` (UPPERCASE)
- **Supporting files**: `lowercase.md` (e.g., `webhook_processing.md`)
- **Variables**: Descriptive names (camelCase for JS, snake_case for Python)

## MCP Tool Usage Patterns

### Finding and Using Nodes

```
1. search_nodes({query: "keyword"})
2. get_node({nodeType: "nodes-base.name"})
3. [Optional] get_node({nodeType: "nodes-base.name", mode: "docs"})
```

### Creating and Validating Workflows

```
1. n8n_create_workflow({name, nodes, connections})
2. validate_workflow({workflow: {...}})
3. n8n_update_partial_workflow({id, operations: [...]})
4. n8n_validate_workflow({id})
5. n8n_update_partial_workflow({id, operations: [{type: "activateWorkflow"}]})
```

### Deploying Templates

```
1. search_templates({searchMode: "by_task", task: "webhook_processing"})
2. n8n_deploy_template({templateId: 123})
```

## Critical nodeType Format Notes

**Two different formats** for different tools:

- **Search/Validate tools**: Use SHORT prefix: `nodes-base.slack`
- **Workflow creation**: Use FULL prefix: `n8n-nodes-base.slack`

This is a common source of errors when creating workflows programmatically.

## Key Statistics

- **Skills**: 7 core skills × 2 locations = 14 implementations
- **Documentation**: 72 markdown files, ~44,000 lines
- **MCP Tools**: 40+ specialized tools
- **Templates**: 2,700+ workflow templates accessible via MCP
- **Supporting Files**: ERROR_PATTERNS.md, COMMON_PATTERNS.md, DATA_ACCESS.md, etc.

## File Structure Summary

```
/
├── .claude/
│   └── skills/          # 7 skills for Claude Code
├── .opencode/
│   ├── skills/          # 7 skills (mirror of .claude/skills)
│   └── package.json     # Plugin dependencies
├── opencode.json        # OpenCode configuration
├── .mcp.json            # MCP server configuration
└── CLAUDE.md            # This file
```

## When to Use This Repository

This repository is used when:

- Building n8n workflows through AI assistance
- Searching for n8n nodes by keyword
- Validating node and workflow configurations
- Deploying workflow templates
- Understanding n8n expression syntax
- Writing JavaScript/Python code in Code nodes
- Debugging workflow validation errors
