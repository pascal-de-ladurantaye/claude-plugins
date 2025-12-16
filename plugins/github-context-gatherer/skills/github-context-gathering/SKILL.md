---
name: GitHub Context Gathering
description: This skill should not be used
version: 0.1.0
---

# GitHub Context Gathering

Gather comprehensive context from GitHub issues and pull requests using `gh view-md` as the primary tool, with intelligent fallback to targeted `gh` commands when output is truncated.

## Core Workflow

### Step 1: Primary Context Gathering

For any GitHub issue or PR URL, start with `gh view-md`:

```bash
gh view-md <github-url>
```

This returns LLM-optimized markdown containing:
- Title, author, creation date, status
- Full description and all comments
- Timeline events (labels, assignments, references)
- For PRs: diffs, review comments, commit history, CI status

### Step 2: Detect Truncation

Check the output for truncation indicators:
- Explicit truncation notice in the output
- Content that appears cut off mid-sentence
- Missing expected sections (e.g., PR with no diff content)

If truncation detected, proceed to Step 4 (Fallback Strategy).

### Step 3: Identify Linked Issues/PRs

Scan the gathered content for links to follow:

**Direct mentions:**
- `#123` or `org/repo#123` patterns in body/comments
- Full GitHub URLs to issues/PRs

**Relationship indicators:**
- "fixes #123", "closes #456", "resolves #789"
- "related to #123", "depends on #456"
- "parent PR", "child PR", "stacked on"

**Cross-references:**
- Timeline events showing linked PRs/issues
- Review comments referencing other PRs

### Step 4: Evaluate Relevance (Smart Detection)

Before following a link, assess whether it's relevant to the original context:

**Follow the link if:**
- Same repository and clearly related topic
- Explicitly marked as dependency/blocker
- Referenced in context of the main issue's solution
- Part of a PR stack (parent/child)

**Stop recursion on this branch if:**
- Different repository with unrelated topic
- Tangential reference (e.g., "similar to how we solved #X")
- Historical reference not relevant to current work
- Meta discussion about process, not content

Use judgment based on the original context. The goal is comprehensive relevant context, not exhaustive link following.

### Step 5: Recursive Gathering

For each relevant linked issue/PR:
1. Run `gh view-md <linked-url>`
2. Track depth (maximum 10 levels)
3. Repeat Steps 2-5 for new links found
4. Build a context tree of gathered information

**Depth tracking:**
- Level 0: Original URL
- Level 1-10: Linked issues/PRs
- Stop at level 10 regardless of remaining links

### Step 6: Handle Images

`gh view-md` downloads images to `/tmp/gh_issue/`. To include visual context:

```bash
# Find downloaded images
ls /tmp/gh_issue/

# Read specific images using the Read tool
# Images are renamed with hashes, check markdown references for mapping
```

Use the Read tool to view images when they contain relevant information (screenshots, diagrams, architecture drawings).

### Step 7: Produce Output

Generate a detailed summary of all gathered context. If a steering prompt was provided, focus the summary accordingly.

**Summary structure:**
1. **Overview**: What the issue/PR is about
2. **Key Findings**: Important details from all gathered sources
3. **Linked Context**: Summary of related issues/PRs and their relevance
4. **Technical Details**: Code changes, implementation specifics
5. **Discussion Highlights**: Key points from comments/reviews
6. **Images**: Description of relevant visual content
7. **Open Questions**: Unresolved issues or missing information

## Fallback Strategy

When `gh view-md` output is truncated, use targeted `gh` commands to get specific data.

### Common Fallback Commands

**Issue details:**
```bash
gh issue view <number> --repo <owner/repo> --json title,body,author,state,labels,comments
```

**PR details:**
```bash
gh pr view <number> --repo <owner/repo> --json title,body,author,state,labels,comments,reviews
```

**PR diff (filenames only for large PRs):**
```bash
gh pr diff <number> --repo <owner/repo> --name-only
```

**Specific file diff:**
```bash
gh pr diff <number> --repo <owner/repo> | grep -A 50 "^diff --git.*<filename>"
```

**PR review comments:**
```bash
gh api repos/<owner>/<repo>/pulls/<number>/comments | jq '.[] | {path, body, user: .user.login}'
```

**Timeline events:**
```bash
gh api repos/<owner>/<repo>/issues/<number>/timeline | jq '.[] | {event, actor: .actor.login}'
```

See `references/fallback-commands.md` for comprehensive fallback command reference.

## Tool Requirements

This skill requires access to:
- **Bash**: Execute `gh view-md`, `gh`, and `jq` commands
- **Read**: Access images in `/tmp/gh_issue/`
- **Glob**: Find downloaded image files

## Additional Resources

### Reference Files

- **`references/gh-view-md.md`** - Detailed gh view-md documentation and options
- **`references/fallback-commands.md`** - Comprehensive gh fallback commands with jq patterns

## Important Notes

**Rate limiting**: GitHub API has rate limits. For large recursive gathering, pace requests appropriately.

**Private repos**: `gh view-md` and `gh` commands respect authentication. Ensure `gh auth status` shows valid login.

**Large diffs**: For PRs with massive diffs, `gh view-md` shows only filenames. Use targeted `gh pr diff` for specific files of interest.

**Context management**: When gathering many linked issues/PRs, prioritize depth over breadth. Go deep on clearly relevant links before exploring tangential ones.
