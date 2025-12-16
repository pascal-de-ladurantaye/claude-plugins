# Fallback Commands Reference

When `gh view-md` output is truncated or specific data is needed, use these targeted `gh` commands with `jq` for precise extraction.

## Issue Commands

### Full issue details
```bash
gh issue view <number> --repo <owner/repo> --json title,body,author,state,labels,assignees,comments,createdAt,updatedAt
```

### Issue body only
```bash
gh issue view <number> --repo <owner/repo> --json body --jq '.body'
```

### Issue comments
```bash
gh issue view <number> --repo <owner/repo> --json comments --jq '.comments[] | "\(.author.login) (\(.createdAt)):\n\(.body)\n---"'
```

### Issue labels
```bash
gh issue view <number> --repo <owner/repo> --json labels --jq '.labels[].name'
```

### Issue timeline
```bash
gh api repos/<owner>/<repo>/issues/<number>/timeline --jq '.[] | select(.event) | "\(.event): \(.actor.login // "system") - \(.created_at)"'
```

### Linked PRs (via timeline)
```bash
gh api repos/<owner>/<repo>/issues/<number>/timeline --jq '.[] | select(.source.issue.pull_request) | .source.issue.html_url'
```

## Pull Request Commands

### Full PR details
```bash
gh pr view <number> --repo <owner/repo> --json title,body,author,state,labels,assignees,comments,reviews,commits,files,createdAt,mergedAt
```

### PR body only
```bash
gh pr view <number> --repo <owner/repo> --json body --jq '.body'
```

### PR comments (conversation)
```bash
gh pr view <number> --repo <owner/repo> --json comments --jq '.comments[] | "\(.author.login) (\(.createdAt)):\n\(.body)\n---"'
```

### PR reviews
```bash
gh pr view <number> --repo <owner/repo> --json reviews --jq '.reviews[] | "\(.author.login) - \(.state):\n\(.body)\n---"'
```

### PR review comments (inline)
```bash
gh api repos/<owner>/<repo>/pulls/<number>/comments --jq '.[] | "\(.path):\(.line // .original_line)\n\(.user.login): \(.body)\n---"'
```

### PR files changed (names only)
```bash
gh pr view <number> --repo <owner/repo> --json files --jq '.files[].path'
```

### PR files with stats
```bash
gh pr view <number> --repo <owner/repo> --json files --jq '.files[] | "\(.path): +\(.additions) -\(.deletions)"'
```

### Full PR diff
```bash
gh pr diff <number> --repo <owner/repo>
```

### Diff for specific file
```bash
gh pr diff <number> --repo <owner/repo> -- <filepath>
```

### PR commits
```bash
gh pr view <number> --repo <owner/repo> --json commits --jq '.commits[] | "\(.oid[0:7]) \(.messageHeadline)"'
```

### PR checks/CI status
```bash
gh pr checks <number> --repo <owner/repo>
```

### PR merge status
```bash
gh pr view <number> --repo <owner/repo> --json mergeable,mergeStateStatus --jq '"\(.mergeable) - \(.mergeStateStatus)"'
```

## Cross-Reference Commands

### Find issues mentioning a term
```bash
gh issue list --repo <owner/repo> --search "<term>" --json number,title,url
```

### Find PRs mentioning a term
```bash
gh pr list --repo <owner/repo> --search "<term>" --json number,title,url
```

### Get linked issues from PR body
```bash
gh pr view <number> --repo <owner/repo> --json body --jq '.body' | grep -oE '(fixes|closes|resolves)\s+#[0-9]+'
```

### Get all issue/PR references in text
```bash
gh pr view <number> --repo <owner/repo> --json body,comments --jq '[.body, .comments[].body] | join("\n")' | grep -oE '#[0-9]+'
```

## Repository Context

### Recent issues
```bash
gh issue list --repo <owner/repo> --limit 20 --json number,title,state,labels
```

### Recent PRs
```bash
gh pr list --repo <owner/repo> --limit 20 --json number,title,state,labels
```

### Issue/PR by label
```bash
gh issue list --repo <owner/repo> --label "<label>" --json number,title,url
gh pr list --repo <owner/repo> --label "<label>" --json number,title,url
```

## Advanced jq Patterns

### Extract all URLs from content
```bash
gh issue view <number> --repo <owner/repo> --json body,comments --jq '[.body, .comments[].body] | join("\n")' | grep -oE 'https://github.com/[^[:space:])>]+'
```

### Get comment authors and dates
```bash
gh issue view <number> --repo <owner/repo> --json comments --jq '.comments | group_by(.author.login) | map({author: .[0].author.login, count: length})'
```

### Find review requests
```bash
gh api repos/<owner>/<repo>/pulls/<number>/requested_reviewers --jq '.users[].login, .teams[].name'
```

### Get PR approval status
```bash
gh pr view <number> --repo <owner/repo> --json reviews --jq '[.reviews[] | select(.state == "APPROVED")] | length'
```

## Error Handling

### Check if issue/PR exists
```bash
gh issue view <number> --repo <owner/repo> --json number 2>/dev/null && echo "exists" || echo "not found"
```

### Handle rate limiting
```bash
gh api rate_limit --jq '.resources.core | "Remaining: \(.remaining)/\(.limit), Resets: \(.reset | todate)"'
```

## Tips

1. **Combine fields**: Request multiple JSON fields in one call to reduce API requests
2. **Use --jq**: Filter server-side when possible for faster responses
3. **Paginate carefully**: Large comment threads may need pagination via `gh api`
4. **Cache results**: For recursive gathering, consider caching already-fetched URLs
5. **Respect rate limits**: Space out requests when gathering many linked issues
