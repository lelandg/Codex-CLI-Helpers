# Codex-CLI-Helpers — agent guide

Documentation-first repo. It publishes tips for Codex CLI and a reusable
"virtual agents" starter package (registry + playbooks). There is no app to
build, test, or run.

## Hard rules

None repo-specific. The global house rules apply.

## Gotchas

- In THIS repo the agents root is `virtual-agents/agents/` (holds
  `virtual-agents/agents/registry.yaml` and `virtual-agents/agents/playbooks/`).
  There is no root-level agents folder here. In every OTHER repo, assume the
  standard root layout: agents/registry.yaml and agents/playbooks/.
- The bootstrap script is `virtual-agents/bootstrap-virtual-agents.sh`. In a
  bootstrapped repo it lands at Scripts/bootstrap-virtual-agents.sh and the
  manual lands at Docs/Virtual-Agents-User-Manual.md (not under Docs/agents/).
- `AGENTS.local.md` is COMMITTED in this repo (unusual). Keep it
  machine-agnostic and free of secrets.
- `virtual-agents/AGENTS.md` and everything under `virtual-agents/` is the
  published starter package. Edit it only when the change is meant to ship to
  consumers.

## Conventions

- Virtual-agent flow: when asked to "use (the) virtual agents" or given a
  playbook name, acknowledge "Using virtual agents (virtual-agents/agents/)."
  (or "(agents/)" in a standard-layout repo), show the quick-help top section
  of `Docs/agents/Virtual-Agents-User-Manual.md`, collect the playbook inputs,
  then run the playbook step by step. Write artifacts to `Docs/` as the
  playbook specifies and append a brief run summary.
- Keep edits small and reviewable (Markdown, YAML, shell). Do not reformat
  unrelated files.
- Commit subjects: short, imperative, optional scope prefix
  (`Docs: clarify setup`, `Agents: add review playbook`).

## Pointers

- Code map: `Docs/CodeMap.md`
- Virtual-agents manual (playbooks, inputs/outputs, trigger phrases):
  `Docs/agents/Virtual-Agents-User-Manual.md`
- Starter package overview: `virtual-agents/README.md`
- Personal working notes: `AGENTS.local.md`

## Scanning & review

Policy lives in `~/.config/agents/AGENTS.md` -> "Dependency, code, and secret
scanning" and "Model delegation & cross-provider review". It is not restated
here; read it there. What is specific to this repo:

- CI runs `gitleaks` on every PR, every push to `main`, and weekly
  (`.github/workflows/security.yml`). There are no dependency manifests here,
  so there is nothing for `npm audit` or `osv-scanner` to scan.
- Dependabot: `github-actions` only (`.github/dependabot.yml`), which keeps the
  workflow's pinned action SHAs current. No package ecosystem, because there is
  no dependency manifest to watch.
- PR reviewers: **Codex** (GPT-6 Astra, run locally against the committed branch
  before opening the PR) and **CodeRabbit** (`coderabbitai[bot]`, re-reviews
  every push — the one to wait on for the head being merged). A green CodeRabbit
  check does not mean a review ran: read the check run's output title, where only
  `Finished` means reviewed. Silence means clean; findings arrive as inline
  comments. `no-ai-review` at PR creation skips the bots.
- The global pre-commit hook runs `gitleaks` and fails closed.
