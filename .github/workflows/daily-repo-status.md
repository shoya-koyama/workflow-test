---
description: |
  This workflow creates daily repo status reports. It gathers recent repository
  activity (issues, PRs, discussions, releases, code changes) and generates
  engaging GitHub issues with productivity insights, community highlights,
  and project recommendations.

on:
  schedule: daily
  workflow_dispatch:

permissions:
  contents: read
  issues: read
  pull-requests: read

network: defaults

tools:
  github:
    lockdown: false

safe-outputs:
  create-issue:
    title-prefix: "[triage] "
    labels: [report, triage]
source: githubnext/agentics/workflows/daily-repo-status.md@d19056381ba48cb1f7c78510c23069701fa7ae87
engine: copilot
---

# Daily Triage Report

Create a daily triage report for maintainers as a GitHub issue.

## Goals

- Help the triage on-call quickly find what to act on today.
- Prioritize items (P0/P1/P2) with brief rationale.
- Keep the report short and actionable.

## Scope / Time window

- Issues/PRs created or updated in the last 24 hours.
- Stale PRs: no updates for 3+ days.
- CI failures: workflow runs failed in the last 24 hours (or latest failure per workflow).

## What to include

### P0 (Urgent / likely impacting users or releases)

- CI failures that block main branch or releases
- Security or outage-related issues (if detected)
- PRs that are merge-ready but blocked by CI or a critical review

### P1 (Important / should be handled soon)

- Untriaged issues (no labels OR no assignee)
- Stale PRs (no activity for 3+ days), especially ones close to merge
- Regressions or bugs with clear reproduction steps

### P2 (Nice to have / backlog grooming)

- Low-severity issues, docs improvements, refactors
- PRs needing minor follow-ups

## Output format

- Use headings: P0 / P1 / P2
- Each bullet must include:
  - Link
  - One-line summary
  - Suggested next action (label / assignee / comment / close / request info)

## Style

- Be concise. No fluff.
- Use emojis sparingly (optional).

