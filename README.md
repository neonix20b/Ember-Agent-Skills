# Ember Agent Skills

Skills for people building applications with
[EmberBSD](https://github.com/oxtech-ember/EmberBSD) and their AI coding assistants,
packaged with the open [Agent Plugins](https://agent-plugins.org/) format and
[Agent Skills](https://agentskills.io/home) for compatible development environments.

Version **0.3.3** includes one skill with focused supporting references:

| Skill | Purpose |
| --- | --- |
| [`emberbsd-repository-guide`](skills/emberbsd-repository-guide/SKILL.md) | Develop applications, add boards, test ports, and contribute reusable fixes with clear evidence |

This version provides repository and contribution workflows. SDK scaffolding, Wasm packaging,
documentation search through MCP, and hardware tools are future integrations.
No MCP server, account connection, or device access is included.

## Purpose and related projects

This repository gives users and AI coding assistants a maintained workflow for
building EmberBSD applications, adapting dependencies and contributing tested
fixes. SDK and Runtime own the application contracts and implementation; skills
help developers use the available tools and understand their actual results.

[EmberBSD](https://github.com/oxtech-ember/EmberBSD#emberbsd-ecosystem) is the
central project and the entry point for the ecosystem.

- [EmberBSD](https://github.com/oxtech-ember/EmberBSD) — OS, drivers, boards and system builds.
- [EmberBSD-Ports](https://github.com/oxtech-ember/EmberBSD-Ports) — third-party recipes, portability patches and native dependencies.
- [EmberBSD-Examples](https://github.com/oxtech-ember/EmberBSD-Examples) — standalone applications and reproducible demonstrations.
- [EmberBSD-Runtime](https://github.com/oxtech-ember/EmberBSD-Runtime) — application execution and device operations; design stage.
- [EmberBSD-SDK](https://github.com/oxtech-ember/EmberBSD-SDK) — application contracts and development tools; design stage.

## Rules for users and their assistants

Start with [developing an application](skills/emberbsd-repository-guide/references/developing-applications.md).
These public instructions work without the maintainers' private wiki or lab.
The repository's root `AGENTS.md` governs work on this plugin's sources; the
installed workflow is in `SKILL.md` and its bundled references. Do not copy our
root `AGENTS.md` over your application's instructions.

| Your task | Assistant workflow |
| --- | --- |
| Build an application using EmberBSD | Work in your repository, follow your conventions, use actual APIs/examples, and document tested build/run commands |
| Add or validate your board | Inspect the nearest platform, integrate kernel/boot/build changes, record hardware evidence, and contribute a board page through a tested PR |
| Fix a reusable defect or add a port | Reproduce, implement, test, and open a focused PR from a contribution branch or fork when publication is authorized |
| Find a bug without a tested fix | Preserve a minimal reproducer and describe the gap; use an authorized issue/report instead of an empty PR |
| Discover a useful workaround or an obsolete instruction | Update the owning documentation and relevant skill reference with evidence, affected versions and a removal condition |

Contributions to EmberBSD use English, retain licenses and provenance, and
include relevant checks. Independently owned applications keep their own
language and licensing choices. A successful build, VM test and physical-board
test support different claims. See the [contribution workflow](skills/emberbsd-repository-guide/references/contributions.md)
for PRs to EmberBSD and submissions to the original upstream.

## Add your board

Developers can use this package to bring their own board to EmberBSD. Start with
the [board catalog](https://github.com/oxtech-ember/EmberBSD/tree/main/ember/boards)
and [OS contribution guide](https://github.com/oxtech-ember/EmberBSD/blob/main/ember/boards/adding-a-board.md).
The installed skill includes [the contributor workflow](skills/emberbsd-repository-guide/references/adding-boards.md).

After loading the skill, open your EmberBSD checkout and ask, for example:

> Use the emberbsd-repository-guide skill to add my board to EmberBSD. It is [model and
> revision] with [SoC], booting through [firmware]. I have [serial console and
> hardware access]. Compare it with existing support, implement the required
> changes, test the available hardware, document the limits, and open a PR.

The workflow covers kernel and device-tree/ACPI changes, firmware/boot selection,
build outputs, validation and public documentation. Your board receives a short
catalog entry and its own capability page. A shared SoC or successful build alone
does not establish hardware support. Firmware, credentials and personalized
images remain subject to their actual licenses and your publication scope.

## Use in your development environment

The package source is
[`oxtech-ember/Ember-Agent-Skills`](https://github.com/oxtech-ember/Ember-Agent-Skills).
Choose the loading method your client documents:

1. **Agent Plugins with skills support:** install or import the repository root,
   which contains `plugin.json` and `skills/`. Select the `emberbsd-development`
   package. Use the client's supported Git, directory or archive installation
   method; the standard does not define a universal install command.
2. **Agent Skills support:** load the complete
   `skills/emberbsd-repository-guide/` directory through the client's skill
   installer or documented search path. Keep `references/` beside `SKILL.md`.
   Copying only the Markdown entry point loses the supporting instructions.
3. **Manual reading:** ask the assistant to read that `SKILL.md` and its linked
   references from a checkout. This supplies instructions for the conversation;
   it does not register the skill for automatic discovery.

Check the official [Agent Plugins client list](https://agent-plugins.org/compatible-clients)
and [Agent Skills client showcase](https://agentskills.io/clients)
for your environment's documentation. Neither listing is a test receipt for
this package. Installation, refresh, permissions and invocation syntax remain
client-specific. Preserve your application's existing instructions.

For automatic discovery, confirm the client lists `emberbsd-repository-guide`
and can read its bundled repository map. Ask, for example:

> Use the emberbsd-repository-guide skill to build a UART decoder in my
> application repository for EmberBSD AArch64. Find a suitable public example,
> check the available interfaces, and document how to build and test it with
> synthetic input. Report separately what still needs a physical board.

Use your client's explicit skill selector if it has one; `$skill-name` is not
required by the portable format. Refresh the installed package through the
same client and verify its version after updates. A source checkout and an
installed copy may be separate.

### Install in Codex

See the [Codex installation and update guide](docs/codex.md) for its marketplace
commands. This repository includes the catalog used by that client, while the
canonical package remains the root Agent Plugins manifest.

### Validation status

Local package checks and native Codex discovery pass for version **0.3.3**.
The latest discovery check used **Codex CLI 0.162.0-alpha.2**; earlier checks
used 0.160.1. These checks do not install into the user's saved configuration
or execute the skill. Installation and behavior in other clients have not
been tested for this release.

## Package structure

```text
.agents/plugins/marketplace.json   Codex marketplace catalog; points to ./
plugin.json                        Agent Plugins manifest; optional client metadata
skills/emberbsd-repository-guide/
  SKILL.md                         Skill instructions and discovery metadata
  agents/openai.yaml               Codex skill presentation
  references/developing-applications.md  User application workflow and scope
  references/adding-boards.md       Board bring-up, evidence and contribution workflow
  references/repositories.md       Public repository ownership map
  references/ports.md              Current tools, porting checks and verified cases
  references/contributions.md      Tested EmberBSD/upstream submission workflow
  references/maintenance.md        Evidence, refresh and workaround retirement
scripts/check-package.rb           Local consistency and native discovery checks
docs/packaging.md                  Portable format and validation boundaries
docs/codex.md                      Codex installation and metadata
LICENSE                           MIT
```

The Codex marketplace catalog and plugin share this repository. Other clients
can load the portable package without using that catalog. A future
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

The Codex check uses a temporary profile and command-line marketplace override.
It does not register or install the plugin in your saved settings. It checks
that Codex discovers the intended plugin identifier and version. It does not
execute the skill or certify acceptance into OpenAI's public directory.

See [portable packaging and validation](docs/packaging.md) before adding skills
or tools. Client-specific setup is documented separately; the package format
and workflow do not require Codex.

## License

[MIT](LICENSE).
