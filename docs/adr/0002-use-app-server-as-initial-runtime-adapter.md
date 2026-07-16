# Use app-server as the initial runtime adapter

ThreadManager will use Codex app-server as its first production integration and
keep its application model independent of app-server protocol types. This gives
the first release thread inventory, residency, relationships, status changes,
and streamed events without coupling the product to internal Rust crates; an
embedded `codex-core-api` adapter remains a future option if app-server cannot
support a required capability.
