# GitHub Code Submission Skill

A provider-neutral agent skill for submitting one coherent code change with durable GitHub tracking.

When the user says “submit this code”, “ship this code”, “deliver this code”, or “提交代码”, the skill treats that request as a narrow authorization bundle:

```text
resolve or create implementation Issue
→ verify the intended change
→ branch, commit, and push
→ resolve or create pull request
→ write delivery evidence back to the Issue
```

The bundle does not authorize merge, deployment, release, force-push, history rewriting, cleanup, repository settings, labels, milestones, projects, or unrelated Issues. Explicit limits such as “commit only” or “do not open a PR” always override the bundle.

## Why this is a separate skill

Requirement planning and code submission have different triggers and authorization models. Keeping this workflow separate prevents ordinary implementation requests from unexpectedly writing GitHub state, while making an explicit submission request fully tracked without repeated approval prompts.

## Behavior

- Reuses a matching open Issue before creating one.
- Reuses the existing PR for the branch before creating one.
- Creates one standalone implementation Issue when no match exists.
- Commits only delivery-related files and never pushes directly to the default branch.
- Links the PR with `Closes #<issue>` and records verification evidence.
- Uses a draft PR when coherent work is reviewable but required evidence is incomplete.
- Stops when multiple Issue or PR candidates are equally plausible.
- Never merges or deploys under the submission authorization.

## Install in Codex

Ask the built-in skill installer:

```text
Use $skill-installer to install https://github.com/merlinz165/github-code-submission/tree/main/skills/github-code-submission
```

Invoke it explicitly with:

```text
$github-code-submission Submit this code.
```

It may also be selected automatically from matching requests.

## Install in Claude Code

This repository includes `.claude-plugin/plugin.json`:

```text
/plugin marketplace add merlinz165/github-code-submission
/plugin install github-code-submission
```

Or copy `skills/github-code-submission` into a skills directory Claude Code scans.

## Install in other Agent Skills clients

Copy the self-contained skill folder into the host's project or user skill root:

```bash
cp -r skills/github-code-submission <skills-root>/github-code-submission
```

## Example prompts

```text
$github-code-submission 提交代码
```

```text
$github-code-submission Ship these changes. Reuse the related Issue and update the current branch's PR.
```

```text
$github-code-submission Submit this code, but do not create a new Issue if no match exists.
```

## Repository structure

```text
.claude-plugin/plugin.json
skills/github-code-submission/
├── SKILL.md
├── agents/openai.yaml
└── references/
    └── submission-workflow.md
```

The skill is instruction-only. It installs no GitHub App, workflow, credential, runtime, or dependency.

## License

MIT
