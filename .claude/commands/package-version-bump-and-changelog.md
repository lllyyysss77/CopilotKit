---
name: package-version-bump-and-changelog
description: Workflow command scaffold for package-version-bump-and-changelog in CopilotKit.
allowed_tools: ["Bash", "Read", "Write", "Grep", "Glob"]
---

# /package-version-bump-and-changelog

Use this workflow when working on **package-version-bump-and-changelog** in `CopilotKit`.

## Goal

Bump package versions and update CHANGELOG.md for all workspace packages in preparation for a release.

## Common Files

- `packages/*/package.json`
- `packages/*/CHANGELOG.md`
- `pnpm-lock.yaml`

## Suggested Sequence

1. Understand the current state and failure mode before editing.
2. Make the smallest coherent change that satisfies the workflow goal.
3. Run the most relevant verification for touched files.
4. Summarize what changed and what still needs review.

## Typical Commit Signals

- Update package.json version for each package
- Update CHANGELOG.md for each package
- Update pnpm-lock.yaml

## Notes

- Treat this as a scaffold, not a hard-coded script.
- Update the command if the workflow evolves materially.