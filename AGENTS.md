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
