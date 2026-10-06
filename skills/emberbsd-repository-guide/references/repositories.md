# EmberBSD repository ownership

These are ownership boundaries, not a support matrix. Inspect the current
checkout and release documentation before relying on an implementation.

| Repository | Owns |
| --- | --- |
| [EmberBSD](https://github.com/apovalixin/EmberBSD) | OS sources, drivers, board support, firmware integration, OS builds and checks |
| [EmberBSD-Examples](https://github.com/neonix20b/EmberBSD-Examples) | Standalone applications and reproducible demonstrations |
| [EmberBSD-Runtime](https://github.com/neonix20b/EmberBSD-Runtime) | Application execution, installation, lifecycle, and shared device operations |
| [EmberBSD-SDK](https://github.com/neonix20b/EmberBSD-SDK) | Application API/ABI, package contracts, developer tools, and compatibility checks |
| [Ember-Agent-Skills](https://github.com/neonix20b/Ember-Agent-Skills) | Developer assistant instructions, tool adapters, and skill packaging |

Examples own executable demonstrations; tutorials explain a learning sequence.
Skills guide the developer's assistant. They are separate from any future agent
running on an EmberBSD device.

The Codex plugin marketplace in this repository distributes developer skills.
An EmberBSD Wasm application catalog would distribute programs for devices and
would use the application contracts owned by SDK and Runtime.

SDK/Runtime instructions require actual released or checked-out interfaces.
Until those exist for a task, use the available OS or example sources and state
the missing contract explicitly. Do not infer an `ember` CLI from project names.
