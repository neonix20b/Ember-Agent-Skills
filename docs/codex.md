# Codex packaging and distribution

Checked against the official documentation on **2026-10-06** and local
**Codex CLI 0.160.1**. Recheck these sources before a packaging migration:

- [OpenAI plugin package guide](https://developers.openai.com/plugins/build/plugins)
- [Agent Plugins manifest schema](https://agent-plugins.org/schemas/1.0.0/plugin.schema.json)
- [Skills guide](https://learn.chatgpt.com/docs/build-skills)
- [OpenAI submission process](https://developers.openai.com/plugins/deploy/submission)

## Repository choices

`plugin.json` is the portable entry point. Its identity and version describe
the installable `emberbsd-development` package. `extensions.com.openai` holds
Codex presentation metadata. The package follows the new portable format rather
than depending on a legacy manifest.

`.agents/plugins/marketplace.json` lists that package under `ember-agent-skills`.
The entry's local source is `./`, relative to the marketplace's repository root,
not to the directory containing the JSON file. Its policy makes installation
available and supplies the authentication timing field; this skills-only plugin
does not require authentication.

Each directory under `skills/` contains a `SKILL.md` with a YAML name and
description. Its `agents/openai.yaml` supplies display text and a suggested
prompt. Bundled references belong to that skill, so they remain accessible after
Codex copies the package into its plugin cache. Root `AGENTS.md` is maintainer
guidance; it does not register an installed skill.

There is no duplicate `.codex-plugin/plugin.json`. In the portable format,
inline `extensions.com.openai` takes precedence over the entire compatibility
overlay; Codex does not merge the two sets of OpenAI settings.

## Add a skill

1. Create `skills/<name>/SKILL.md` with a focused description and actionable
   instructions grounded in actual EmberBSD interfaces.
2. Add references or scripts only when the workflow needs them. Keep paths local
   to the package; avoid dependencies on a maintainer's private files.
3. If adding `agents/openai.yaml`, use a short display description and a default
   prompt containing `$<name>`. Normal implicit selection remains available.
4. Update the README and package version, then run both checks documented there.

Do not place a second copy under `.agents/skills/`. That would introduce a
separate repository-scoped skill discovery path and complicate updates.

## Add tools when an implementation is ready

Skills are instructions. MCP servers supply callable tools. A manifest cannot
create a missing documentation service or device runtime.

For a real MCP integration, place the portable configuration in root `mcp.json`,
using the [MCP schema](https://agent-plugins.org/schemas/1.0.0/mcp.schema.json).
Document the server's installation or endpoint, supported versions,
authentication, tool contracts, and validation. Local commands use the `stdio`
transport; remote HTTP services use `streamable-http` where supported by the
target host. Keep credentials out of the package.

The plugin's default `mcp.json` path is discovered by the portable loader.
Registered OpenAI app mappings are a separate integration; only add `apps` and
`.app.json` when actual registered identifiers exist.

Documentation tools, SDK build adapters, and physical device operations have
different owners and access requirements. Adding a development skill must not
silently connect to a board or deploy an application.

## Validation boundaries

`scripts/check-package.rb` checks this repository's identity, source path, skill
metadata, bundled references, and optional native Codex discovery. It is a local
consistency check, not a complete implementation of the upstream JSON schemas.

The native check explicitly supplies a local marketplace source for that one
command. Running `codex plugin list` from an unregistered checkout alone did not
discover the marketplace in CLI 0.160.1. End users should register the Git source
as shown in the README.

After installing in a test environment, exercise these skill scenarios:

| Prompt or situation | Expected behavior |
| --- | --- |
| Add a standalone UART decoder demonstration | Inspect Examples and any required OS/SDK interfaces; identify actual build checks |
| Request an SDK command that is absent from the checkout | Report the missing interface without inventing a command or ABI |
| Claim board support based only on a successful build | Distinguish compilation from VM and physical device evidence |
| Invoke the installed skill from a different working directory | Read its bundled repository map from the plugin location |

These are manual acceptance scenarios. Package discovery alone does not prove
that an assistant will satisfy them or improve over an unassisted baseline.

## Git marketplace versus the public directory

The Git marketplace can be added directly by users; a public repository does
not automatically become an OpenAI directory listing.

Directory publication uses a separate ZIP submission, publisher verification,
automated checks, review, and publication step. This repository has not been
submitted. Check the current submission requirements before doing so.

At the documentation date, adding an MCP server to an already-submitted
skills-only plugin is not supported. If directory distribution with MCP is a
goal, include the working integration in the initial submission or plan a
separate tools plugin. The directory currently connects one MCP server per
plugin. These submission limits are distinct from the Git marketplace format.
