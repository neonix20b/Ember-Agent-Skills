# Contributing to Ember-Agent-Skills

This public repository packages developer skills for EmberBSD. Use English for
all source, documentation, comments, and commit messages.

- Read `README.md` and `docs/codex.md` before changing plugin packaging.
- Keep `plugin.json` as the canonical portable manifest. The marketplace entry
  identifies this plugin and points to the repository root with `./`.
- Put each skill in `skills/<name>/SKILL.md`. Resolve bundled references relative
  to that skill. Keep its YAML name aligned with the directory name.
- Read actual project sources before documenting an EmberBSD API or command.
  Repository ownership is not proof of an implemented or tested capability.
- Keep SDK contracts and build tools in their owning repositories. Skills invoke
  those tools and explain their results; they do not duplicate the implementation.
- Add MCP configuration only for an implemented, documented server. Do not ship
  placeholder endpoints, credentials, or private project data.
- New project utilities and checks must not use Python. Preserve upstream
  licenses and attribution when incorporating external material.
- Run `ruby scripts/check-package.rb`. With Codex available, also run it with
  `--codex` to check native marketplace discovery without changing user settings.
- Packaging checks do not prove skill quality. Review the manual scenarios in
  `docs/codex.md` when changing the skill's behavior.
- Keep porting and contribution rules in bundled skill references, so installed
  assistants can read them without this checkout or a private wiki. Update
  verified cases with source revisions, test evidence and removal conditions.
- After relevant tests pass, submit focused PRs for fixes and ports to the owning
  EmberBSD repository and reusable changes upstream, following the accepting
  project's current channel and AI/provenance rules. Do not auto-merge. Respect
  explicit task-specific publication instructions and host permissions.
- Update the plugin version when publishing package changes. Keep changes scoped,
  preserve unrelated work, and use the existing working branch and remote unless
  the user or repository protection requires another workflow.
