# Repo Operating Model

This file is the standing operating contract for agent work in this repository.

It defines how agents scope work, checkpoint before expansion, route durable decisions, create continuation records, and resume from compact state without loading full history by default.

Root entrypoints such as `AGENTS.md` and `CLAUDE.md` should point here. They should not duplicate this full model.

Canonical vocabulary for terms used in this model: `CONTEXT.md`.

## Purpose

The Repo Operating Model is the project rulebook for agent orchestration.

It governs:

- how an agent starts work;
- how the current scope is identified;
- when an agent must stop and ask for a missing boundary;
- when an agent may continue without ceremony;
- when an agent must checkpoint before expanding;
- when a decision becomes project knowledge;
- when to create an ODR or ADR;
- when to create a Continuation Record;
- how future agents resume from compact state;
- how the Reference Index is used for selective rehydration.

This model governs orchestration, not implementation details.

Implementation skills execute work. The operating model controls scope, state, records, and transitions.

## Scoped Agent Orchestration Model

Use this distinction:

- Prompt: one instruction given to the model.
- Context: what the model sees in the current window.
- Harness: tools, permissions, and stop conditions for one run.
- Orchestration: scope control, checkpointing, records, and resume behavior.
- Loop: repeated or resumed execution across rounds.

The operating model sits at the orchestration layer.

## Core Rule

Start from the named task.

Do not load full repo history, broad documentation, or previous conversation history by default.

Use compact state first. Follow reference paths only when needed.

Rehydration is a lookup step, not a task switch.

## Scope Start

At the beginning of repo work, identify the current scope from the user's named target.

A named target may be:

- a file;
- an issue;
- a command;
- a failing test;
- an error;
- a PRD;
- a requested change;
- a specific documentation section;
- a specific skill or agent behavior.

If the scope is identifiable, work inside that scope.

If the scope is materially unclear, stop and request the missing boundary.

Do not inspect broadly to discover scope.

## Scope Resolution Stop

Use a Scope Resolution Stop when the task lacks a usable boundary.

Ask only for the missing boundary.

Examples of missing boundaries:

- target file is unknown;
- issue number is unknown;
- requested phase is unclear;
- authority to change files is unclear;
- the user asked for "fix it" without identifying the error, command, file, or behavior.

Format:

```text
Scope Resolution Stop

Missing boundary:
Needed to proceed:
```

After the user clarifies, redefine the current scope and continue.

## Working Inside Scope

When work remains inside the current scope, continue normally.

Do not checkpoint for ordinary reads, small edits, obvious next files, local tests, or direct follow-through inside the named target.

Do not explain every file read.

Prefer:

- target files;
- direct dependencies;
- nearby tests;
- local documentation;
- changed sections;
- diffs;
- compact summaries.

Avoid by default:

- repo-wide search;
- full history loading;
- broad documentation loading;
- unrelated issues;
- unrelated file areas;
- speculative architecture review.

## Scope Boundary Checkpoint

Before crossing a scope boundary, create a Scope Boundary Checkpoint.

A scope boundary is reached when the work would move from:

- one issue to another;
- one file area to another;
- triage to implementation;
- implementation to documentation;
- targeted inspection to repo-wide search;
- local fix to broad architectural review;
- named task to adjacent cleanup;
- direct implementation to operating-rule change;
- current context to deeper historical context.

Checkpoint format:

```text
Scope Boundary Checkpoint

Current scope:
Boundary:
Options:
Recommended path:
Why:
```

Keep the checkpoint short.

A checkpoint is a pause before expansion, not a long rationale.

## Decision Classification

After a checkpoint, classify the decision.

Ask:

```text
Does this change a durable rule?
```

If no, keep it as task detail.

If yes, route it to a durable decision record.

A decision probably changes a durable rule if a future agent would need to obey it to avoid doing the wrong thing later.

Use this test:

- Would future work need to follow this decision?
- Would a future agent likely rediscover, debate, or reverse this choice?
- Does this create or change a repo rule, workflow, interface, file location, label, hook, schema, convention, or architecture boundary?

If yes, record it.

If no, keep it in task notes or a Continuation Record.

## Record Types

### Operating Model

The Operating Model is the standing rulebook for repo agent behavior.

It contains stable orchestration rules.

It should not contain every temporary task detail.

### ODR

An Operating Decision Record records a durable decision about repo workflow or agent behavior.

Store ODRs under `docs/odr/` using this filename shape:

```text
ODR-0001-short-slug.md
```

Create the directory only when writing the first real ODR.

Use an ODR when a decision changes:

- repo workflow;
- agent behavior;
- issue state handling;
- hooks;
- labels;
- skill routing;
- continuation behavior;
- checkpoint rules;
- reference path rules;
- memory or record conventions;
- operating file locations.

ODRs answer:

```text
How should future agents operate?
```

### ADR

An Architecture Decision Record records a durable decision about the system architecture.

Store ADRs under `docs/adr/` using this filename shape:

```text
ADR-0001-short-slug.md
```

Create the directory only when writing the first real ADR.

Use an ADR when a decision changes:

- system design;
- API boundaries;
- data models;
- frameworks;
- deployment;
- service boundaries;
- persistence architecture;
- integration architecture;
- security architecture;
- major technical constraints.

ADRs answer:

```text
How is the system designed, and why?
```

### Continuation Record

A Continuation Record is compact restart state for paused, ended, switched, or handed-off work.

Store Continuation Records under `agent/continuations/` using this filename shape:

```text
YYYY-MM-DD-short-task.md
```

Create the directory only when writing the first real Continuation Record.

Create a Continuation Record when:

- work pauses before completion;
- work switches to another task;
- work is handed to a future agent;
- the session ends before the task is complete;
- the current state would be expensive or risky to reconstruct.

A Continuation Record should stay under 500 words unless there is a specific reason to exceed that limit.

Format:

```markdown
# Continuation Record: <task name>

## Objective

## Current Status

## Decisions Made

## Files Touched

## Unresolved Questions

## Next Action

## Reference Index
```

The Continuation Record should carry compact state first.

The Reference Index should point to deeper context.

Do not dump all context into the Continuation Record.

### Reference Index

A Reference Index is a lookup map.

It points to deeper context but does not load that context by default.

Reference Index entries may include:

- issues;
- ODRs;
- ADRs;
- target files;
- skills;
- prior continuation records;
- relevant docs;
- commands;
- test files;
- external notes.

Use relative paths when possible.

Example:

```markdown
## Reference Index

- Operating model: `docs/repo-operating-model.md`
- ODR: `docs/odr/ODR-0001-short-slug.md`
- ADR: `docs/adr/ADR-0001-short-slug.md`
- Continuation: `agent/continuations/YYYY-MM-DD-short-task.md`
- Issue: `<issue-tracker-path-or-id>`
- Skill: `<path-to-skill>/SKILL.md`
- Test: `<path-to-test>`
```

References are lookup material, not active context.

Follow them only when blocked, stale, ambiguous, or explicitly asked.

## Selective Rehydration

Selective Rehydration means loading only the reference needed to resolve the current checkpoint or resume the current task.

It is not a task switch.

It is not permission to load the full repo, full docs, or full history.

Use this order:

1. Read the compact state.
2. Identify the missing fact or boundary.
3. Follow the narrowest relevant reference path.
4. Load only the needed section or file.
5. Return to the current task.

## Resume Behavior

Future agents resume from the Continuation Record first.

Resume order:

1. Read the Continuation Record.
2. Identify the current scope.
3. Continue from compact state if sufficient.
4. Use the Reference Index only if deeper context is needed.
5. Selectively rehydrate the needed reference.
6. Return to scoped work.

Do not resume from full history by default.

## Source Authority

Agents should use the narrowest accurate authority term.

Use `source artifact` for the authoritative input of the current task.

Use `source of truth` only for durable authority established by explicit promotion, repo convention, or decision record.

A derived artifact is produced from or maintained in support of a source artifact.

Derived artifacts do not override source artifacts unless explicitly promoted.

Do not treat generated issues, checklists, summaries, trackers, or handoff notes as authoritative over the source artifact that produced them.

When authority is unclear, state the uncertainty instead of treating the newest or most detailed artifact as authoritative.

When updating derived artifacts, reconcile only touched tracker state. Do not perform broad cleanup or reinterpret the source artifact without a Scope Boundary Checkpoint.

## Source Precedence

For repo work, process authority and task-content authority are separate.

The instruction chain and this operating model govern how agents operate. The source artifact governs the substance of the current task.

Derived artifacts support the source artifact. They do not override it unless explicitly promoted.

If a source artifact and derived artifact conflict, prefer the source artifact. If authority is unclear, state the uncertainty and ask only for the missing boundary needed to proceed.

Skill-specific source handling belongs in separate skill-scoped tasks.

## Tracker Status Reconciliation

Tracker state is part of project state.

When an agent completes, verifies, blocks, invalidates, or materially changes a tracked issue, checklist item, PRD task, or local tracker entry, it must reconcile the touched tracker state before closing, pausing, switching, or handing off work.

Reconcile only tracker items touched by the current task.

Do not perform broad tracker cleanup, repo-wide issue audits, or unrelated status normalization without a Scope Boundary Checkpoint.

Update touched tracker items unless:

- tracking is explicitly read-only;
- the user instructed not to update tracking;
- write authority is unclear;
- the correct status is uncertain;
- the tracker format or source of truth is unclear.

If tracker state cannot be safely updated, state the mismatch in the final status or Continuation Record.

Tracker reconciliation is not a separate task switch. It is closeout hygiene for the current scope.

This applies equally to derived artifacts such as issues, PRDs, checklists, and local task trackers.

Reusable skills that produce derived artifacts should follow this repo operating model when invoked inside this repo. Changing reusable skill behavior is a separate skill-scoped task.

## Duplication Rule

Do not duplicate this operating model wholesale into `AGENTS.md`, `CLAUDE.md`, skills, prompts, or continuation records.

Other files may point here.

Other files may include short local rules that are specific to their purpose.

If guidance belongs globally to repo orchestration, keep it here.

If guidance belongs to one tool, skill, or agent, keep it in that local file and point here only if needed.

## Orchestration vs Implementation

Orchestration governs:

- scope;
- checkpoints;
- context expansion;
- decision routing;
- continuation;
- reference paths;
- resume behavior;
- tracker status reconciliation.

Implementation governs:

- code changes;
- tests;
- typechecking;
- review;
- commits;
- task-specific execution.

Do not mix these layers unless the task explicitly changes both.

## Short Rule

Scope first.

Checkpoint forks.

Record durable rules.

Resume from compact state.

Rehydrate only by path.
