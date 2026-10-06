# Ember Agent Skills

Skills for people building applications with
[EmberBSD](https://github.com/apovalixin/EmberBSD) and their AI coding assistants,
packaged as an installable Codex plugin and a Git-backed plugin marketplace.

Version **0.2.2** includes one skill with focused supporting references:

| Skill | Purpose |
| --- | --- |
| [`emberbsd-repository-guide`](skills/emberbsd-repository-guide/SKILL.md) | Develop applications, locate real interfaces, test ports, and contribute reusable fixes with clear evidence |

This version provides repository and contribution workflows. SDK scaffolding, Wasm packaging,
documentation search through MCP, and hardware tools are future integrations.
No MCP server, account connection, or device access is included.

## Purpose and related projects

This repository gives users and AI coding assistants a maintained workflow for
building EmberBSD applications, adapting dependencies and contributing tested
fixes. SDK and Runtime own the application contracts and implementation; skills
help developers use the available tools and understand their actual results.

[EmberBSD](https://github.com/apovalixin/EmberBSD#emberbsd-ecosystem) is the
central project and the entry point for the ecosystem.

- [EmberBSD](https://github.com/apovalixin/EmberBSD) — OS, drivers, boards and system builds.
- [EmberBSD-Ports](https://github.com/neonix20b/EmberBSD-Ports) — third-party recipes, portability patches and native dependencies.
- [EmberBSD-Examples](https://github.com/neonix20b/EmberBSD-Examples) — standalone applications and reproducible demonstrations.
- [EmberBSD-Runtime](https://github.com/neonix20b/EmberBSD-Runtime) — application execution and device operations; design stage.
- [EmberBSD-SDK](https://github.com/neonix20b/EmberBSD-SDK) — application contracts and development tools; design stage.

## Rules for users and their assistants

Start with [developing an application](skills/emberbsd-repository-guide/references/developing-applications.md).
These public instructions work without the maintainers' private wiki or lab.
The repository's root `AGENTS.md` governs work on this plugin's sources; the
installed workflow is in `SKILL.md` and its bundled references. Do not copy our
root `AGENTS.md` over your application's instructions.

| Your task | Assistant workflow |
| --- | --- |
| Build an application using EmberBSD | Work in your repository, follow your conventions, use actual APIs/examples, and document tested build/run commands |
| Fix a reusable defect or add a port | Reproduce, implement, test, and open a focused PR from a contribution branch or fork when publication is authorized |
| Find a bug without a tested fix | Preserve a minimal reproducer and describe the gap; use an authorized issue/report instead of an empty PR |
| Discover a useful workaround or an obsolete instruction | Update the owning documentation and relevant skill reference with evidence, affected versions and a removal condition |

Contributions to EmberBSD use English, retain licenses and provenance, and
include relevant checks. Independently owned applications keep their own
language and licensing choices. A successful build, VM test and physical-board
test support different claims. See the [contribution workflow](skills/emberbsd-repository-guide/references/contributions.md)
for PRs to EmberBSD and submissions to the original upstream.

## Install in Codex

Use a Codex version with `codex plugin marketplace` support. The package and
command syntax were checked with **Codex CLI 0.160.1**. Native discovery was
verified without installing into the maintainer's saved configuration.

```sh
codex plugin marketplace add neonix20b/Ember-Agent-Skills --ref main
codex plugin list --marketplace ember-agent-skills --available --json
codex plugin add emberbsd-development@ember-agent-skills
```

The first command registers the source, the second lists its plugins, and the
third installs the selected plugin. The listing should contain
`emberbsd-development@ember-agent-skills` at version `0.2.2`.
Start a new conversation in your application project after installation.
In the desktop app, check the Plugins view for the installed package.

| Name | Meaning |
| --- | --- |
| `Ember-Agent-Skills` | GitHub repository |
| `ember-agent-skills` | Marketplace identifier |
| `emberbsd-development` | Plugin identifier |
| `emberbsd-development@ember-agent-skills` | Fully qualified installation identifier |

Try a prompt such as:

> Use $emberbsd-repository-guide to build a UART decoder in my application
> repository for EmberBSD AArch64. Find a suitable public example, check the
> available interfaces, and document how to build and test it with synthetic
> input. Report separately what still needs a physical board.

Codex may also select the skill from its description when an EmberBSD task
matches. The installed host controls skill selection and available tools.

Additional starting prompts:

> Update this EmberBSD port to the current stable release. Use
> $emberbsd-repository-guide, inspect pkgsrc and pkgsrc-wip, fix compatibility,
> and test the package and a runtime scenario before opening a PR from my fork.

> Use $emberbsd-repository-guide to turn this reproduced build failure into a
> tested fix, prepare the EmberBSD and upstream submissions, and update the
> affected developer instructions.

The workflow records original sources and SHA256, keeps a coherent toolchain,
and requires real test evidence before a ready PR. Upstream submission follows
the target project's actual channel and AI-assistance rules.

If the plugin command is unavailable, check `codex --version` and
`codex plugin --help`; use a host that supports this package format. If the
skill is missing after installation, check the installed package in Plugins
and start a new conversation. Merely cloning this repository does not install
the skill in an unrelated application project.

To refresh the Git marketplace snapshot:

```sh
codex plugin marketplace upgrade ember-agent-skills
```

Catalog refresh and the installed plugin copy are separate. After a release,
check the installed version in Plugins and reinstall the plugin if it still
shows the old version. Start a new conversation to use the updated skills.

## Package structure

```text
.agents/plugins/marketplace.json   Marketplace catalog; points to ./
plugin.json                        Portable plugin manifest and Codex metadata
skills/emberbsd-repository-guide/
  SKILL.md                         Skill instructions and discovery metadata
  agents/openai.yaml               Codex skill presentation
  references/developing-applications.md  User application workflow and scope
  references/repositories.md       Public repository ownership map
  references/ports.md              Current tools, porting checks and verified cases
  references/contributions.md      Tested EmberBSD/upstream submission workflow
  references/maintenance.md        Evidence, refresh and workaround retirement
scripts/check-package.rb           Local consistency and native discovery checks
docs/codex.md                      Packaging rules and validation boundaries
LICENSE                           MIT
```

The marketplace and its initial plugin share this repository. There is no need
for a separate catalog repository to distribute this one plugin. A future
EmberBSD Wasm marketplace would distribute device applications, a different
kind of package.

## Validate a checkout

Ruby with its standard library is sufficient for the consistency checks:

```sh
ruby scripts/check-package.rb
```

To additionally check discovery with your installed Codex CLI:

```sh
ruby scripts/check-package.rb --codex
```

The Codex check passes a temporary command-line configuration override. It does
not register or install the plugin in your saved settings. It checks that Codex
discovers the intended plugin identifier and version. It does not execute the
skill or certify acceptance into OpenAI's public directory.

See [the Codex packaging guide](docs/codex.md) before adding skills or tools.

For another development assistant, use its documented Agent Skills mechanism
to load the complete `skills/emberbsd-repository-guide/` directory, including
references. If it only supports project instructions, explicitly ask it to read
the checkout's `SKILL.md` and linked references. This is a manual fallback, not
automatic discovery. Only Codex discovery is currently verified; Cursor and
Claude Code installation have not been tested. Keep relative paths intact and
preserve your project's existing instructions.

## License

[MIT](LICENSE).
