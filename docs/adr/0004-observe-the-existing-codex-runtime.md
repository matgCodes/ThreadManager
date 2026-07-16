# Observe the existing Codex runtime

ThreadManager must observe the active Codex desktop runtime the user is already
working in rather than launch an independent app-server process as its source
of live state. If the desktop runtime does not expose a supported connection,
the integration must remain an explicit research or prototype gap instead of
silently presenting a separate runtime as the Now View.
