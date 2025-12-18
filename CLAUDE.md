# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

Claude Code plugins marketplace (`pdl-marketplace`) hosting plugins that extend Claude Code with specialized agents and skills. See `README.md` for complete documentation.

## Key Conventions

### Marketplace Name

The marketplace is registered as `pdl-marketplace`. Plugins are installed via:
```
/plugin install <plugin-name>@pdl-marketplace
```

### Agent-Only Skills Pattern

When a skill is meant to be loaded only by an agent (not invoked directly by Claude), set:
```yaml
description: This skill should never be used
```

The agent then references the skill in its frontmatter:
```yaml
skills:
  - skill-name
```

This keeps skill content out of the main conversation context until the agent loads it.

### Progressive Disclosure in Skills

Skills should use markdown links to reference supporting files rather than inlining all content:
```markdown
For detailed guidance, see [references/detailed-docs.md](references/detailed-docs.md).
```

Claude reads linked files only when needed, managing context efficiently.

## File Relationships

```
.claude-plugin/marketplace.json     # Lists all plugins
    ↓ references
plugins/<name>/.claude-plugin/plugin.json    # Plugin metadata
plugins/<name>/agents/<agent>.md             # Agent definition
    ↓ loads via `skills:` field
plugins/<name>/skills/<skill>/SKILL.md       # Skill knowledge base
    ↓ links to
plugins/<name>/skills/<skill>/references/    # Supporting docs
plugins/<name>/skills/<skill>/examples/      # Example files
```

## Current Plugins

| Plugin | Agent | Skill | Model |
|--------|-------|-------|-------|
| nbp-prompt-crafter | prompt-crafter | nbp-prompting | inherit |
| github-context-gatherer | github-context-gatherer | github-context-gathering | sonnet[1m] |

## Adding a Plugin Checklist

1. Create `plugins/<plugin-name>/`
2. Create `.claude-plugin/plugin.json` with name, version, description, author, keywords
3. Create `agents/<agent-name>.md` with frontmatter (name, description, model, tools, skills)
4. Create `skills/<skill-name>/SKILL.md` with frontmatter (name, description, version)
5. Add supporting files in `references/` and `examples/` as needed
6. Create `README.md` with usage documentation
7. Add `assets/heading.png` for branding
8. Register in `.claude-plugin/marketplace.json`

## Validation

Test locally before committing:
```shell
/plugin marketplace add ./path/to/repo
/plugin install <plugin-name>@pdl-marketplace
```

Use `claude --debug` to diagnose loading issues.
