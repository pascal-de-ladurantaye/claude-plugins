# gh view-md Reference

## Overview

`gh view-md` is a GitHub CLI extension that fetches issues and pull requests, rendering them as markdown optimized for LLM consumption.

## Installation

```bash
gh extension install joshbeckman/gh-view-md
```

## Command Syntax

```bash
gh view-md <github_issue_or_pr_url> [options]
```

## Options

| Option | Description |
|--------|-------------|
| `--max-diff LINES` | Maximum number of diff lines to show for PRs (default: 800) |
| `-h, --help` | Display help |

## Output Content

### For Issues

- Title, author, creation date, status
- Full description (body)
- All comments with timestamps
- Timeline events:
  - Label additions/removals (🏷️)
  - Assignments (👤)
  - Cross-references
  - Status changes

### For Pull Requests

Everything from issues, plus:
- Code diffs (up to `--max-diff` lines)
- Review comments inline with diff context
- Commit history
- CI/check status
- Merge status

## Output Format

```markdown
# Issue/PR Title

**Author:** @username | **Created:** 2024-01-15 | **Status:** open

## Description

[Full body content]

## Comments

### @commenter - 2024-01-16 10:30

[Comment content]

## Timeline

- 🏷️ @user added label `bug`
- 👤 @user assigned @assignee

## Diff (for PRs)

```diff
[Diff content]
```
```

## Link Enhancement

Bare GitHub URLs in content are automatically converted to markdown links with titles:
- Input: `https://github.com/owner/repo/issues/123`
- Output: `[Issue Title](https://github.com/owner/repo/issues/123)`

## Image Handling

Images are downloaded locally to `/tmp/gh_issue/`:
- Both GitHub-hosted images and external images
- Markdown references updated to local paths
- Supports private repository images (uses gh auth)

Example:
- Original: `![screenshot](https://user-images.githubusercontent.com/...)`
- Downloaded to: `/tmp/gh_issue/abc123.png`
- Updated reference: `![screenshot](/tmp/gh_issue/abc123.png)`

## Large Diff Handling

When PR diffs exceed `--max-diff` lines:
- Only filenames are shown, not full diffs
- Use targeted `gh pr diff` for specific files

Example output for large PR:
```
## Changed Files (diff truncated, showing filenames only)

- src/components/Button.tsx
- src/utils/helpers.ts
- tests/button.test.ts
```

## Common Usage Patterns

### Basic issue fetch
```bash
gh view-md https://github.com/owner/repo/issues/123
```

### PR with extended diff
```bash
gh view-md https://github.com/owner/repo/pull/456 --max-diff 2000
```

### Capture to file
```bash
gh view-md https://github.com/owner/repo/issues/123 > issue.md
```

## Troubleshooting

### "gh: command not found"
Install GitHub CLI: https://cli.github.com/

### "gh-view-md: command not found"
Install extension: `gh extension install joshbeckman/gh-view-md`

### Authentication errors
Run `gh auth status` and `gh auth login` if needed

### Rate limiting
GitHub API limits apply. Wait and retry, or authenticate for higher limits.
