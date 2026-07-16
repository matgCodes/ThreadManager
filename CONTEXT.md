# ThreadManager

ThreadManager presents Codex runtime state so a user can understand what work
exists and what is happening without changing that runtime state.

## Language

**Observation**:
Reading and presenting Codex runtime state without changing a thread, turn, or
agent.
_Avoid_: Management, control

**Navigation**:
Opening or focusing an existing Codex task for inspection without changing its
runtime state.
_Avoid_: Resume, steer

**Control Action**:
An operation that changes Codex runtime state, such as resuming, interrupting,
archiving, spawning, steering, or messaging.
_Avoid_: Navigation

**Host Inventory**:
The complete set of Codex work visible to ThreadManager on the selected local
host.
_Avoid_: Current task, current project

**Now View**:
The default view that prioritizes Tasks currently executing, loaded, waiting,
or in error so the user can see what is happening in Codex now.
_Avoid_: Recent tasks, Host Inventory

**Project**:
A user-recognizable workspace used to organize related Codex work.
_Avoid_: Directory, repository

**Session**:
A related tree of Codex work consisting of one root and any descendant work it
creates.
_Avoid_: Project, process

**Task**:
The user-facing presentation of a Logical Agent in ThreadManager.
_Avoid_: Worker, process

**Logical Agent**:
A durable task identity containing its task path, thread ID, metadata, and
persisted history. It survives runtime unloading but not explicit closure or
deletion.
_Avoid_: Permanent agent, resident thread

**Loaded Agent**:
The residency state of a Logical Agent whose thread is currently held in the
ThreadManager. A Loaded Agent may be idle and consume no execution capacity.
_Avoid_: Separate agent, active agent

**Executing Agent**:
The execution state of a Loaded Agent that is processing a turn and consuming
execution capacity.
_Avoid_: Active agent

**Residency**:
Whether a Logical Agent's thread is loaded into the ThreadManager.
_Avoid_: Execution, activity

**Execution Capacity**:
The runtime's concurrency allowance for agents processing turns, managed
separately from residency capacity.
_Avoid_: Thread limit, memory capacity

**Observed State**:
A runtime state explicitly confirmed by the Codex runtime serving the current
Now View.
_Avoid_: Inferred state, estimated state

**Unknown State**:
The explicit state shown when the active Codex runtime cannot confirm a Task's
residency or execution state.
_Avoid_: Assumed idle, stale state
