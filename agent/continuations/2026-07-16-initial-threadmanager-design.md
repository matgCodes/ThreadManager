# Continuation Record: Initial ThreadManager design

## Objective

Define a bounded read-only ThreadManager and preserve an integration seam for
future Multi-Agent V2 support.

## Current Status

The first grilling round is complete. Product boundaries, the runtime-state
model, initial integration, and first host decisions are recorded. No
implementation or UI prototype exists.

## Decisions Made

- First release is a read-only observer with navigation, not Control Actions.
- Now View prioritizes executing, loaded, waiting, and error Tasks; Host
  Inventory remains available with Project and Session grouping/filtering.
- A Task is the user-facing Logical Agent. Loaded Agent and Executing Agent are
  residency and execution states of that same identity.
- App-server is the initial adapter; the application model remains
  transport-neutral for possible embedded-core support later.
- First host is a movable standalone utility window with Keep on Top support.
  Codex embedding is deferred pending a supported extension point.
- Live state must come from the existing Codex desktop runtime. Unknown is
  shown when state cannot be confirmed; state is never inferred.

## Files Touched

- `CONTEXT.md`
- `docs/adr/0001-separate-agent-identity-residency-and-execution.md`
- `docs/adr/0002-use-app-server-as-initial-runtime-adapter.md`
- `docs/adr/0003-separate-ui-from-host-shell.md`
- `docs/adr/0004-observe-the-existing-codex-runtime.md`
- `docs/adr/0005-do-not-infer-runtime-state.md`

## Unresolved Questions

- Can an external client attach to the existing Codex desktop runtime through a
  supported app-server socket or bridge?
- Which UI technology should host the movable utility window?
- How should protocol Active states map to Executing versus waiting substates?
- Should Keep on Top be enabled by default and persist across launches?
- What navigation mechanism can open the selected Task in Codex?

## Next Action

Run a targeted research/prototype session to verify attachment to the existing
Codex desktop runtime. Resume grilling with that evidence before choosing the
UI technology or writing a spec.

## Reference Index

- Operating model: `docs/repo-operating-model.md`
- Domain language: `CONTEXT.md`
- Architecture decisions: `docs/adr/`
- Upstream source: `https://github.com/openai/codex`
- Repository: `https://github.com/matgCodes/ThreadManager`
