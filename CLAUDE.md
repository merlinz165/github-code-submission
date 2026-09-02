# CLAUDE.md

This repository is an agent skill package, not an application. It has no runtime, build system, or test suite; the product is the provider-neutral instruction text under `skills/github-code-submission/`.

## Structure

```text
.claude-plugin/plugin.json
skills/github-code-submission/
├── SKILL.md
├── agents/openai.yaml
└── references/
    └── submission-workflow.md
```

`SKILL.md` defines discovery, bundled authorization, and non-negotiable boundaries. `references/submission-workflow.md` owns the detailed operational sequence. Host-specific metadata belongs outside the shared instructions.

## Editing rules

- Keep the workflow provider-neutral; do not bake Codex-only or Claude-only behavior into `SKILL.md` or `references/`.
- Preserve the narrow meaning of “submit/ship/deliver code”: one implementation Issue, one delivery branch and commit set, one PR, and evidence written back to the Issue.
- Explicit exclusions always override the submission bundle.
- Never expand the bundle to merge, deploy, release, force-push, rewrite history, delete branches or worktrees, modify repository governance, or create unrelated GitHub artifacts.
- Keep reuse-before-create behavior for both Issues and PRs.
- Preserve unrelated dirty and untracked work.
- Update README and host metadata when public behavior, paths, or installation changes.

## Validation

Run the Skill Creator validator against `skills/github-code-submission/`, then check Markdown links, JSON syntax, `git diff --check`, and repository status. Do not claim end-to-end GitHub testing unless a real submission run has been completed.
