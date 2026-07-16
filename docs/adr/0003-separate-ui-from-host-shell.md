# Separate the UI from its host shell

ThreadManager's main UI will be independent of the shell that presents it. The
first host is a standalone movable utility window that can be positioned
anywhere on screen; embedding inside Codex is deferred until a supported
extension point is verified, allowing a future embedded host without rewriting
the inventory UI or application model.
