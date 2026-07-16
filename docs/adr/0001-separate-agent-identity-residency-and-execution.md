# Separate agent identity, residency, and execution

ThreadManager models each Task as a durable Logical Agent and represents Loaded
Agent and Executing Agent as residency and execution states of that same
identity, not as separate agents. This matches Multi-Agent V2's separate agent
registry, LRU residency management, and execution limiter, allowing completed
agents to remain useful without occupying memory or execution capacity and
preventing the UI model from coupling identity to runtime state.
