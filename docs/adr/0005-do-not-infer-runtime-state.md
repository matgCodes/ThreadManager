# Do not infer runtime state

ThreadManager will display residency and execution state only when the active
Codex runtime explicitly confirms it, and will show Unknown when that state is
unavailable. It will not infer Loaded or Executing from timestamps, recent
messages, persisted history, or other indirect signals because a live monitor
that presents stale inference as runtime truth would undermine the Now View.
