# Claude Code Plugin Marketplace

A collection of plugins for [Claude Code](https://claude.ai/code) that extend its capabilities with specialized agents and skills.

## Available Plugins

| Plugin | Description |
|--------|-------------|
| [nbp-prompt-crafter](plugins/nbp-prompt-crafter) | Crafts optimized image generation prompts for Nano-Banana Pro (Google Gemini) following official prompting best practices |
| [github-context-gatherer](plugins/github-context-gatherer) | Recursively gathers GitHub context from issues and pull requests using `gh view-md` for rich, LLM-optimized markdown output |

## Installation

### Add the Marketplace

```shell
/plugin marketplace add pascal-de-ladurantaye/claude-plugins
```

### Install a Plugin

```shell
/plugin install nbp-prompt-crafter@pdl-marketplace
```

Or browse available plugins interactively:

```shell
/plugin
```

## Plugin Development

### Creating a New Plugin

1. Create a directory under `plugins/<plugin-name>/`

2. Add the plugin manifest at `.claude-plugin/plugin.json`:

```json
{
  "name": "my-plugin",
  "version": "1.0.0",
  "description": "What this plugin does",
  "author": {
    "name": "Your Name"
  },
  "keywords": ["relevant", "keywords"]
}
```

3. Register in `.claude-plugin/marketplace.json`:

```json
{
  "name": "my-plugin",
  "source": "./plugins/my-plugin",
  "description": "Brief description"
}
```

### Plugin Directory Structure

```
plugins/<plugin-name>/
├── .claude-plugin/
│   └── plugin.json          # Plugin manifest (required)
├── agents/                   # Subagent definitions
│   └── <agent-name>.md
├── skills/                   # Agent skills
│   └── <skill-name>/
│       ├── SKILL.md         # Skill definition (required)
│       ├── references/      # Supporting documentation
│       └── examples/        # Example files
├── commands/                 # Slash commands (optional)
│   └── <command-name>.md
├── hooks/                    # Event handlers (optional)
│   └── hooks.json
├── assets/                   # Plugin branding
│   └── heading.png
└── README.md                # Plugin documentation
```

### Agent Definition Format

Create markdown files in `agents/` with YAML frontmatter:

```markdown
---
name: my-agent
description: When Claude should invoke this agent. Be specific about triggers.
model: sonnet | opus | haiku | inherit
color: cyan | blue | green | yellow | red | magenta
tools:
  - Read
  - Grep
  - Glob
  - Bash
  - Edit
  - Write
skills:
  - my-skill-name
---

System prompt for the agent goes here. Describe the agent's role,
workflow, and how it should approach tasks.
```

**Model Options:**
- `sonnet` - Default, balanced capability
- `opus` - Most capable
- `haiku` - Fastest, lightweight tasks
- `inherit` - Use same model as main conversation
- `sonnet[1m]` - Sonnet with extended context

**Available Tools:** Read, Write, Edit, Glob, Grep, Bash, WebFetch, WebSearch, TodoWrite, Task, AskUserQuestion, and MCP server tools.

### Skill Definition Format

Create `SKILL.md` in `skills/<skill-name>/`:

```markdown
---
name: My Skill Name
description: Brief description. Set to "This skill should never be used" for agent-only skills.
version: 1.0.0
allowed-tools: Read, Grep, Glob  # Optional: restrict available tools
---

# Skill Title

Knowledge base content in markdown. This is loaded into the agent's
context when the skill is referenced.

## Sections

Organize with headers for progressive disclosure.

## References

Link to supporting files:
- See [references/detailed-docs.md](references/detailed-docs.md)
- Examples in [examples/sample-prompts.md](examples/sample-prompts.md)
```

**Skill Invocation:**
- Skills are model-invoked (Claude decides when to use them)
- Set description to indicate non-use for agent-bundled skills
- Reference supporting files for progressive context loading

### Command Definition Format

Create markdown files in `commands/`:

```markdown
---
description: Brief description shown in /help
---

# Command Name

Instructions for what Claude should do when this command is invoked.
```

Commands are user-invoked via `/command-name`.

### Hook Configuration

Create `hooks/hooks.json` for event handlers:

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Write|Edit",
        "hooks": [
          {
            "type": "command",
            "command": "${CLAUDE_PLUGIN_ROOT}/scripts/format.sh"
          }
        ]
      }
    ]
  }
}
```

**Available Events:** PreToolUse, PostToolUse, PermissionRequest, UserPromptSubmit, Notification, Stop, SubagentStop, SessionStart, SessionEnd, PreCompact

### Testing Locally

```shell
# Add local marketplace for development
/plugin marketplace add ./path/to/claude-plugins

# Install plugin
/plugin install my-plugin@pdl-marketplace

# Make changes, then reinstall
/plugin uninstall my-plugin@pdl-marketplace
/plugin install my-plugin@pdl-marketplace
```

Use `claude --debug` to see plugin loading details and troubleshoot issues.

## Architecture

### Marketplace Registry

`.claude-plugin/marketplace.json` defines available plugins:

```json
{
  "name": "pdl-marketplace",
  "owner": {
    "name": "Pascal de Ladurantaye"
  },
  "plugins": [
    {
      "name": "plugin-name",
      "source": "./plugins/plugin-name",
      "description": "Plugin description"
    }
  ]
}
```

### Plugin Manifest Schema

`.claude-plugin/plugin.json` in each plugin:

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `name` | string | Yes | Unique identifier (kebab-case) |
| `version` | string | No | Semantic version |
| `description` | string | No | Brief explanation |
| `author` | object | No | `{name, email, url}` |
| `keywords` | array | No | Discovery tags |
| `homepage` | string | No | Documentation URL |
| `repository` | string | No | Source code URL |
| `license` | string | No | SPDX identifier |

### Environment Variables

- `${CLAUDE_PLUGIN_ROOT}` - Absolute path to plugin directory. Use in hooks and scripts for portable paths.

## Resources

- [Claude Code Plugins Documentation](https://code.claude.com/docs/en/plugins)
- [Plugin Technical Reference](https://code.claude.com/docs/en/plugins-reference)
- [Plugin Marketplaces Guide](https://code.claude.com/docs/en/plugin-marketplaces)
- [Subagents Documentation](https://code.claude.com/docs/en/sub-agents)
- [Agent Skills Guide](https://code.claude.com/docs/en/skills)

## License

MIT
