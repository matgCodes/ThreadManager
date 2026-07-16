# ThreadManager Agent Instructions

## Project Purpose

ThreadManager is a local visual interface for inspecting Codex thread identity,
residency, and activity.

The initial product scope is a useful thread manager. Preserve a clean runtime
integration seam so Multi-Agent V2 support can be added later without rewriting
the user interface or application model. Record durable integration and
architecture choices as ADRs rather than embedding them in this file.

## Project Sources

- Repository operating rules: `docs/repo-operating-model.md`
- Issue-tracker workflow: `docs/agents/issue-tracker.md`
- Triage-label mapping: `docs/agents/triage-labels.md`
- Domain-document conventions: `docs/agents/domain.md`
- Canonical domain vocabulary: `CONTEXT.md`, once created through domain modeling
- Durable architecture decisions: `docs/adr/`, created when the first ADR is written
- Active work and planning: GitHub Issues for `matgCodes/ThreadManager`

Keep setup, development, and verification commands in the README or a focused
runbook once the implementation toolchain is selected.

## Agent skills

### Issue tracker

Track work in GitHub Issues for `matgCodes/ThreadManager`. External pull requests
are reviewed separately and are not a triage request surface. See
`docs/agents/issue-tracker.md`.

### Triage labels

Use the canonical `needs-triage`, `needs-info`, `ready-for-agent`,
`ready-for-human`, and `wontfix` labels. See `docs/agents/triage-labels.md`.

### Domain docs

Use the single-context layout: root `CONTEXT.md` plus repository-wide ADRs under
`docs/adr/`. See `docs/agents/domain.md`.

## Repo Operating Model

For repo work, follow `docs/repo-operating-model.md` after applying this local `AGENTS.md`.

Keep this file as the local entrypoint and instruction map. Do not duplicate the full operating model here.

## Local Constraints

- Verify current Codex behavior against the installed protocol schemas, official
  documentation, or the upstream `openai/codex` source before relying on it.
- Keep credentials and tokens out of the repository. Use macOS Keychain or an
  approved secret store.
- Keep raw transport-specific Codex types behind the selected runtime adapter.
  The exact adapter architecture remains an ADR decision.

## What Does Not Belong Here

- Full workflow procedures already contained in the repo operating model
- Feature plans, ticket bodies, and temporary work status
- Copied upstream Codex documentation or source
- Secrets, credentials, generated protocol dumps, or machine-specific state
