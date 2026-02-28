---
name: weekly-recap
description: Generate a weekly activity recap from GitHub PRs and git history
disable-model-invocation: true
allowed-tools: Bash
argument-hint: [username]
---

Generate a weekly activity recap for the past week. Use the GitHub username `$ARGUMENTS` if provided, otherwise detect it with `gh api user`.

## Steps

1. **Determine the user and date range**
   - Get the GitHub username (from argument or `gh api user --jq '.login'`)
   - Calculate last week's Monday–Sunday date range

2. **Fetch GitHub PRs**
   - PRs authored by the user, updated last week: `gh pr list --search "author:<user> updated:<start>..<end>" --state all`
   - PRs reviewed by the user, updated last week: `gh pr list --search "reviewed-by:<user> updated:<start>..<end>" --state all`
   - Include: number, title, state, createdAt, mergedAt, url, headRefName

3. **Search git history**
   - Get all commits by the user from last week across all branches: `git log --author="<user>" --since="<start>" --until="<end>" --format="%h %ad %s" --date=short --all`
   - Sort by date

4. **Present the summary**
   - **PRs Authored**: table with #, title, state, merged date
   - **PRs Reviewed**: table with #, title, author, state, merged date (exclude self-authored)
   - **Daily Breakdown**: group commits by day, summarize what was worked on
   - **Overall Summary**: 2-3 sentence high-level summary of the week's focus areas
