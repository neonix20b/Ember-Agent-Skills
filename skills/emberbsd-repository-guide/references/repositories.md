# EmberBSD repository ownership

These are ownership boundaries, not a support matrix. Inspect the current
checkout and release documentation before relying on an implementation.

| Repository | Owns |
| --- | --- |
| [EmberBSD](https://github.com/oxtech-ember/EmberBSD) | OS sources, drivers, board support, firmware integration, OS builds and checks |
| [EmberBSD-Ports](https://github.com/oxtech-ember/EmberBSD-Ports) | Third-party recipes, source hashes, portability patches, pkgsrc overlays, common dependency profiles, and package build probes |
| [EmberBSD-Examples](https://github.com/oxtech-ember/EmberBSD-Examples) | Standalone applications and reproducible demonstrations |
| [EmberBSD-Runtime](https://github.com/oxtech-ember/EmberBSD-Runtime) | Application execution, installation, lifecycle, and shared device operations |
| [EmberBSD-SDK](https://github.com/oxtech-ember/EmberBSD-SDK) | Application API/ABI, package contracts, developer tools, and compatibility checks |
| [Ember-Agent-Skills](https://github.com/oxtech-ember/Ember-Agent-Skills) | Developer assistant instructions, tool adapters, and skill packaging |

Examples own executable demonstrations; tutorials explain a learning sequence.
Start from the [central project map](https://github.com/oxtech-ember/EmberBSD)
and verify current repository contents. Ports owns adaptations to external
software; changes to kernel interfaces remain in the OS repository.
Skills guide the developer's assistant. They are separate from any future agent
running on an EmberBSD device.

The Codex plugin marketplace in this repository distributes developer skills.
An EmberBSD Wasm application catalog would distribute programs for devices and
would use the application contracts owned by SDK and Runtime.

SDK/Runtime instructions require actual released or checked-out interfaces.
Until those exist for a task, use the available OS or example sources and state
the missing contract explicitly. Do not infer an `ember` CLI from project names.
