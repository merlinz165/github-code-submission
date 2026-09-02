# Tracked Code Submission Workflow

Use this workflow only for the single delivery unit authorized by the user's code-submission request.

## 1. Establish the Submission Baseline

Read repository instructions before acting. Inspect:

- repository root, GitHub remote, and authenticated GitHub access;
- default branch, current branch, upstream, worktrees, and status;
- staged, unstaged, untracked, and branch-versus-base diffs;
- the user's requested outcome and any referenced Issue or PR;
- relevant implementation, tests, product documents, and recent commits;
- open Issues and PRs that may already represent the delivery.

Separate the intended delivery files from unrelated user work. If the code contains multiple independently deliverable outcomes, present the proposed split and stop before GitHub writes; one invocation should not manufacture a misleading umbrella Issue or PR.

Do not treat an existing local commit, branch name, or PR description as sufficient proof of requirements. Verify load-bearing claims against current code and available evidence.

## 2. Resolve or Create the Implementation Issue

Choose the Issue in this order:

1. an open Issue explicitly named by the user, if it matches the code;
2. an open Issue linked by the current branch, commits, or existing PR, if it matches;
3. one clearly matching open implementation Issue found by searching titles and bodies;
4. otherwise, a new standalone implementation Issue for this delivery unit.

If several candidates match, stop and ask the user to choose. If the closest Issue is closed and the code adds new work, link the closed Issue as history and create a new implementation Issue instead of silently reopening or rewriting completed work.

Create or update the selected Issue so another agent can understand the delivery without the original conversation. Preserve existing human-authored decisions and discussion. Prefer targeted body edits or a progress comment over replacing the Issue's meaning.

The Issue should capture:

- outcome and affected behavior;
- current verified state;
- scoped requirements represented by the code;
- acceptance scenarios;
- verification expected or completed;
- relevant code and document paths;
- explicit non-goals and unavailable evidence.

Do not create an Epic, labels, milestone, project entry, decision Issue, or speculative follow-up Issue under the submission bundle. If a missing product decision materially affects public behavior, data ownership, security, architecture, migration, billing, destructive behavior, or acceptance criteria, record the ambiguity on the implementation Issue and stop before committing or pushing.

Read the Issue back and verify its repository, number, state, title, and content before referencing it elsewhere.

## 3. Verify the Delivery

Run checks proportionate to the changed behavior and repository risk. Prefer the repository's established commands. Include as applicable:

- focused behavior or regression tests;
- broader tests for shared contracts;
- type checking, lint, formatting, and production build;
- migrations, generated artifacts, or configuration validation;
- runtime or visual evidence required by acceptance scenarios;
- `git diff --check` and a final status review.

Record exact commands and outcomes. Distinguish failures introduced by this change from pre-existing failures and unavailable checks.

Do not submit unsafe, incoherent, or unreviewable work merely to finish the workflow. When the change is coherent but verification is incomplete for a known reason, it may be submitted as a draft PR with the gap recorded prominently on both the PR and Issue.

## 4. Prepare the Branch and Commit

Reuse the clearly related feature branch when it is safe. If the work is on the default branch or a branch unrelated to the delivery, create a feature branch using repository conventions; otherwise default to:

```text
feature/issue-<number>-<short-slug>
```

Before staging, review the exact intended file list. Stage only delivery-related files. Preserve unrelated modifications and untracked files in place.

Commit using the repository's convention and reference the Issue. If no convention exists, use a concise Conventional Commit subject and include `Refs #<number>` in the body. Do not amend unrelated commits, rewrite history, force-push, or include secrets.

Push the delivery branch and verify that the remote head equals the intended local commit.

## 5. Resolve or Create the Pull Request

If the pushed branch already has an open PR for this outcome, update that PR. Do not create a second PR for the same branch. Otherwise create a PR against the verified default branch.

The PR body should include:

- concise outcome summary;
- linked implementation Issue with `Closes #<number>`;
- acceptance scenarios covered;
- exact verification commands and results;
- known gaps or unavailable evidence;
- compatibility, migration, or rollout notes when relevant;
- explicit non-goals when they prevent scope confusion.

Use a draft PR when required verification is incomplete or the delivery is not ready for review. Do not describe a draft or failing change as ready.

Read the PR back and verify its repository, number, state, base branch, head branch, current head commit, and Issue-closing link.

## 6. Update the Issue with Delivery Evidence

After the PR exists, update the Issue with the branch, commit, PR link, verification results, and any unresolved gaps. Avoid duplicating information already represented by native GitHub links unless the evidence would otherwise be lost.

Read the Issue back once more and confirm that it points to the current PR and does not claim completion before merge.

## 7. Handle Unavailable Remote Writes

If GitHub access, authentication, permissions, or network access prevents a required mutation:

- preserve any safe local work already completed;
- prepare complete Issue or PR drafts when useful;
- do not invent remote URLs or claim that GitHub state changed;
- report the failed operation, available evidence, and exact next action.

Do not switch remotes, repositories, accounts, or authentication configuration without explicit user authorization.

## Completion Result

Report:

- Issue number, URL, and whether it was created or updated;
- branch and commit;
- PR number, URL, state, and whether it was created or updated;
- verification commands and results;
- excluded files and preserved unrelated work when relevant;
- unresolved decisions, failures, or unavailable evidence;
- confirmation that merge, deployment, release, and cleanup were not performed.
