![image](assets/heading.png)

# GitHub Context Gatherer

A Claude Code plugin that recursively gathers GitHub context from issues and pull requests using `gh view-md` for rich, LLM-optimized markdown output.

## Features

- **Rich context extraction**: Uses `gh view-md` to get full issue/PR content including comments, timeline, diffs, and review comments
- **Intelligent fallback**: When output is truncated, falls back to targeted `gh` commands with `jq` for specific data
- **Recursive gathering**: Follows linked issues/PRs up to 10 levels deep, stopping when links become unrelated to the original context
- **Image support**: Reads downloaded images from `/tmp/gh_issue/` for visual context
- **Flexible output**: Provides detailed summaries steered by optional user prompts

## Prerequisites

- [GitHub CLI](https://cli.github.com/) (`gh`) installed and authenticated
- [gh-view-md](https://github.com/joshbeckman/gh-view-md) extension installed:
  ```bash
  gh extension install joshbeckman/gh-view-md
  ```
- `jq` for JSON processing (for fallback commands)

## Components

### Skill: `github-context-gathering`

Core knowledge for gathering GitHub context. Not meant to be used by anything but the agent.

### Agent: `github-context-gatherer`

Autonomous agent (sonnet model) that gathers comprehensive GitHub context. Triggers when:
- User pastes a GitHub URL and asks about it
- User mentions needing "full context" on an issue/PR
- Explicitly requested


## How It Works

1. **Primary**: Runs `gh view-md <url>` to get comprehensive markdown output
2. **Link detection**: Identifies linked issues/PRs in the content
3. **Relevance check**: Determines if linked items are related to the original context
4. **Recursion**: Gathers related links up to 10 levels deep
5. **Fallback**: If output is truncated, uses targeted `gh` commands for specific data
6. **Image access**: Reads any downloaded images from `/tmp/gh_issue/`
7. **Summary**: Provides detailed summary based on gathered context and optional steering prompt
