---
name: github-code-submission
description: Submit or ship a coherent code change with automatic GitHub tracking. Use when the user asks to submit, ship, deliver, or “提交代码”, or explicitly wants the current changes committed and represented by a related GitHub Issue and pull request. Reuse or update matching artifacts before creating new ones. Do not use for ordinary implementation, requirement decomposition, review-only work, local commits that explicitly exclude GitHub, merging, deployment, or release.
metadata:
  short-description: Submit code with automatic GitHub Issue and PR tracking
---

# GitHub Code Submission

Turn one coherent code delivery into durable GitHub state. Treat the user's explicit request to submit, ship, or deliver code as authorization for the narrow submission bundle below, without asking separately for each included step.

## Submission Bundle

The bundle authorizes, for the requested delivery unit:

1. create or update one related implementation Issue;
2. create or reuse a non-default delivery branch;
3. stage and commit only the related changes;
4. push that branch;
5. create or update its pull request;
6. record the PR and verification evidence on the Issue.

Explicit user constraints override the bundle. “Commit only”, “do not push”, “no Issue”, “no PR”, or an equivalent instruction removes that step. The bundle never authorizes merging, deployment, release, production changes, branch or worktree deletion, force-push, history rewriting, repository settings, labels, milestones, projects, or unrelated Issues.

Read [references/submission-workflow.md](references/submission-workflow.md) and follow it completely before mutating GitHub.

## Non-Negotiable Boundaries

- Resolve the repository, remote, default branch, instructions, Git state, and exact delivery files before writing anything.
- Preserve unrelated dirty and untracked work. Never sweep it into the submission or discard it.
- Prefer an explicit or clearly matching open Issue and the existing PR for the branch. Do not create duplicates for convenience.
- Stop for user choice when multiple Issues, PRs, or delivery units are equally plausible.
- Ground Issue and PR content in the current request, code, diff, tests, and repository documents. Do not invent requirements or claim unavailable evidence.
- Never push delivery commits directly to the default branch.
- Verify every remote mutation by reading it back. Report URLs only for artifacts that actually exist.

## Completion Standard

Submission is complete only when the intended files are committed on the pushed delivery branch, one related open Issue records the work, one PR targets the verified default branch and links that Issue, and the reported verification belongs to the PR's current head. Otherwise report the exact stopping point and next safe action.
