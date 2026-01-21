# AGENTS.md - n8n-mcp OpenCode Plugin

**Documentation standards for coding agents working on this repository**

Last updated: 2026-01-22

---

## Repository Overview

This is an **OpenCode plugin repository** for n8n-mcp integration, containing:

- `.opencode/agents/` - Agent definitions (currently: n8n.md)
- `.opencode/skills/` - Skill documentation modules (7 specialized skills)
- `opencode.json` - MCP server configuration for n8n API integration
- **No traditional source code** - This is a documentation-driven architecture
- All content is Markdown-based skill and agent documentation

---

## Build/Test/Validation Commands

### No Traditional Build System

This repository has **no package.json, tsconfig.json, or test suites** at the root level.

### Validation Commands

```bash
# Validate Markdown syntax (if markdownlint is installed)
markdownlint .opencode/**/*.md

# Validate JSON configuration
cat opencode.json | jq .

# Check file structure
find .opencode/skills -name "SKILL.md" | wc -l  # Should be 7
find .opencode/agents -name "*.md" | wc -l      # Should be 1+

# Verify frontmatter in skills
head -5 .opencode/skills/*/SKILL.md | grep "^name:"

# Verify frontmatter in agents
head -20 .opencode/agents/*.md | grep "^description:"
```

### Testing Skills Locally

1. Load the skill in OpenCode using the `/skill` command
2. Test activation with trigger keywords from README.md
3. Verify cross-references between skills work correctly
4. Check that examples render properly in OpenCode UI

---

## Documentation Style Guidelines

### Frontmatter Standards

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

### Markdown Conventions

**Section Hierarchy:**
```markdown
## Main Section (Title Case)

### Subsection (Title Case)

#### Sub-subsection (less common)
```

**Horizontal Rules:**
```markdown
---
```
Use between major sections for visual separation.

**Code Blocks:**
Always specify language:
```markdown
```javascript
// JavaScript example
```

```json
// JSON example
```

```bash
# Bash command
```
```

**Comparison Examples:**
```markdown
// ❌ WRONG: Description of the mistake
const bad = example;

// ✅ CORRECT: Description of the right way
const good = example;
```

**Tables:**
```markdown
| Column 1 | Column 2 | Column 3 |
|----------|----------|----------|
| Data     | Data     | Data     |
```

**Lists:**
- Use `-` for unordered lists
- Use `1.` for ordered lists (auto-numbering)
- Use `- [ ]` for checklists

**Links:**
- Internal: `[SKILL.md](SKILL.md)` or `[ERROR_PATTERNS.md](ERROR_PATTERNS.md)`
- External: `[n8n Docs](https://docs.n8n.io/)`
- Section links: `#section-heading-kebab-case`

### Content Patterns

**Always Include:**
1. **Quick Start/Quick Reference** - First practical section
2. **Error Prevention** - Common mistakes with ❌/✅ examples
3. **Best Practices** - Production-tested recommendations
4. **Integration Section** - How this skill relates to others

**When Available:**
- Usage statistics: "38% of failures", "7,841 occurrences"
- Performance metrics: "<20ms", "100-500ms average"
- Decision shortcuts: "When to use X vs Y"
- Production examples from real workflows

**Example Structure:**
```markdown
## Pattern Name

**Use when**: Clear use case description

**Example**:
```javascript
const example = 'production code';
```

**Key techniques**:
- Technique 1
- Technique 2

**Common mistakes**:
- ❌ WRONG: Anti-pattern
- ✅ CORRECT: Best practice
```

### Emoji Usage

Use **sparingly** for emphasis:
- ✅ CORRECT / GOOD - For approved patterns
- ❌ WRONG / BAD - For anti-patterns
- ⚠️ CRITICAL / WARNING - For critical warnings
- 🔍 - For search/discovery sections (rare)

**Do NOT overuse** - reserve for important comparisons and warnings.

---

## Skill Structure Standards

### Required Files

Every skill must have:

1. **SKILL.md** (400-700 lines typical)
   - Main content with comprehensive guidance
   - Quick start section
   - Detailed explanations
   - Examples and patterns
   - Error prevention
   - Best practices
   - Integration with other skills

2. **README.md** (250-350 lines typical)
   - Skill metadata and overview
   - Purpose statement
   - Activation triggers/keywords
   - What you'll learn
   - File structure diagram
   - Coverage summary
   - When to use this skill
   - Success metrics
   - Related documentation links

### Optional Supporting Files

Based on skill complexity:
- `COMMON_PATTERNS.md` - Collection of production patterns (e.g., 10 patterns)
- `ERROR_PATTERNS.md` - Top errors with solutions and percentages
- `DATA_ACCESS.md` - Specific data access patterns
- `BUILTIN_FUNCTIONS.md` - Reference documentation
- `DEPENDENCIES.md` - Property dependencies
- `OPERATION_PATTERNS.md` - Operation-specific configs
- `VALIDATION_GUIDE.md` - Validation workflows
- `[TOPIC].md` - Any domain-specific guides

### Skill Naming Conventions

**Format**: `n8n-[domain]-[subdomain]`

**Examples**:
- `n8n-code-javascript` - JavaScript in Code nodes
- `n8n-code-python` - Python in Code nodes  
- `n8n-mcp-tools-expert` - MCP tool usage
- `n8n-validation-expert` - Validation workflows
- `n8n-expression-syntax` - n8n expression language
- `n8n-node-configuration` - Node config patterns
- `n8n-workflow-patterns` - Workflow architectures

**Always use kebab-case** for skill identifiers.

### Cross-Referencing Skills

Every skill should have an **"Integration with Other Skills"** section:

```markdown
## Integration with Other Skills

### n8n Expression Syntax
- **Distinction**: Expressions use `{{}}` in OTHER nodes
- **When to use**: Template strings vs JavaScript code

### n8n MCP Tools Expert
- Find nodes: `search_nodes({query: "keyword"})`
- Get configuration: `get_node({nodeType})`

### n8n Validation Expert
- Validate configurations before deployment
- Handle validation errors
```

**Reference specific files**:
```markdown
**See**: [DATA_ACCESS.md](DATA_ACCESS.md) for comprehensive guide
**See**: [ERROR_PATTERNS.md](ERROR_PATTERNS.md) #3 for detailed solutions
```

---

## Agent Definition Standards

### Frontmatter Requirements

```yaml
---
description: >-
  Multi-line agent description explaining when to use.
  
  <example>
  Context: The user wants to [scenario].
  User: "User quote"
  Assistant: "Agent quote"
  </example>
  
  <example>
  Context: The user has [problem].
  User: "User quote"
  Assistant: "Agent quote"
  </example>
mode: all
color: "#ff0000"
---
```

### Content Structure

**1. Core Principles Section:**
```markdown
## Core Principles

### 1. Principle Name

CRITICAL: Key behavior rule.

❌ BAD: Anti-pattern example
✅ GOOD: Correct pattern example
```

**2. Workflow Process Section:**
```markdown
## Workflow Process

1. **Phase Name** (context)
   - Action 1
   - Action 2
   - Pattern example

2. **Next Phase** (context)
   - Action 1
   - Action 2
```

**3. Critical Warnings:**
```markdown
### ⚠️ Never Trust Defaults

Explain the danger with examples.

```json
// ❌ FAILS at runtime
{bad: "example"}

// ✅ WORKS - explicit config
{good: "example", with: "all params"}
```
```

**4. Tool Execution Examples:**
```markdown
// STEP 1: Discovery (parallel execution)
[Silent execution]
search_nodes({query: 'keyword', includeExamples: true})
search_templates({searchMode: 'by_task'})

// Response after all tools complete:
"Results summary"
```

### Agent Best Practices

1. **Silent Execution** - Tools run without commentary
2. **Parallel Operations** - Independent calls in parallel
3. **Statistics** - Include real data: "2,709 templates available"
4. **Batch Operations** - Show multi-operation examples
5. **Response Templates** - Provide exact format examples

---

## Examples & Error Handling

### Example Format

```markdown
### Error #1: Missing Return Statement (38%)

**Problem**: Code executes but returns nothing.

**Example**:
```javascript
// ❌ WRONG: No return statement
const items = $input.all();
// ... processing ...
// Forgot to return!

// ✅ CORRECT: Always return data
const items = $input.all();
// ... processing ...
return items.map(item => ({json: item.json}));
```

**Why it matters**: Next nodes expect data. Missing return causes workflow failure.

**Fix**: Always end Code nodes with explicit return statement.
```

### Error Documentation Standards

- **Include frequency** when known: "38% of failures", "Most common mistake"
- **Provide context**: Why the error happens
- **Show fixes**: Clear before/after examples
- **Explain impact**: What breaks when error occurs
- **Prevention**: How to avoid in first place

---

## Naming Conventions

### Files
- **UPPERCASE.md** - Key documentation files (SKILL.md, README.md, ERROR_PATTERNS.md)
- **lowercase.md** - Supporting topic files (webhook_processing.md, ai_agent_workflow.md)

### Sections
- **## Title Case** - For main section headers
- **### Title Case** - For subsection headers
- Use descriptive, specific names

### Code Examples
- **Use descriptive variable names**: `activeUsers`, `totalRevenue` (not `a`, `t`, `x`)
- **Follow language conventions**: camelCase for JavaScript, snake_case for Python
- **Be consistent**: Use same naming style throughout examples

### Skills & Agents
- **Skills**: `n8n-domain-subdomain` (kebab-case)
- **Agents**: Descriptive filename like `n8n.md`
- **IDs**: Match filename without extension

---

## No Cursor/Copilot Rules Found

- ❌ No `.cursorrules` file in repository
- ❌ No `.cursor/rules/` directory
- ❌ No `.github/copilot-instructions.md` file

**This AGENTS.md serves as the primary guidance for coding agents.**

---

## Quick Reference Checklist

Before creating/editing skills or agents, verify:

- [ ] **Frontmatter present** - YAML with required fields
- [ ] **Sections properly hierarchical** - ## → ### → ####
- [ ] **Code blocks specify language** - ```javascript, ```json, ```bash
- [ ] **Examples use ❌/✅ pattern** - Clear wrong vs right
- [ ] **Cross-references work** - Links to related skills/files
- [ ] **Integration section included** - How skill relates to others
- [ ] **Descriptive variable names** - No single-letter variables in examples
- [ ] **Error percentages included** - When statistics available
- [ ] **Production examples** - Real-world patterns, not toy examples
- [ ] **Horizontal rules separate sections** - Visual organization with ---

---

## Additional Resources

### Existing Documentation
- **Agent Example**: `.opencode/agents/n8n.md` (433 lines) - Comprehensive agent pattern
- **Skill Example**: `.opencode/skills/n8n-code-javascript/SKILL.md` (700 lines) - Full skill structure
- **Supporting Docs**: See any skill's supporting files for deep-dive patterns

### External References
- **OpenCode Docs**: https://opencode.ai/docs
- **n8n Documentation**: https://docs.n8n.io/
- **MCP Documentation**: For understanding MCP server integration

---

**Ready to create or edit n8n-mcp OpenCode plugin documentation!** Follow these standards to maintain consistency with existing skills and agents.
