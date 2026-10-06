# Ember Agent Skills

Developer skills for [EmberBSD](https://github.com/apovalixin/EmberBSD), packaged
as an installable Codex plugin and a Git-backed plugin marketplace.

Version **0.2.0** includes one skill with focused supporting references:

| Skill | Purpose |
| --- | --- |
| [`emberbsd-repository-guide`](skills/emberbsd-repository-guide/SKILL.md) | Locate the owner, use current tools, adapt and test ports, prepare contributions, and distinguish source, build, VM, and hardware evidence |

This version provides repository and contribution workflows. SDK scaffolding, Wasm packaging,
documentation search through MCP, and hardware tools are future integrations.
No MCP server, account connection, or device access is included.

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
third installs the selected plugin. Start a new conversation after installation.
In the desktop app, check the Plugins view for the installed package.

| Name | Meaning |
| --- | --- |
| `Ember-Agent-Skills` | GitHub repository |
| `ember-agent-skills` | Marketplace identifier |
| `emberbsd-development` | Plugin identifier |
| `emberbsd-development@ember-agent-skills` | Fully qualified installation identifier |

Try a prompt such as:

> Use $emberbsd-repository-guide to decide where a new UART decoder example
> belongs and which interfaces and checks already exist.

Codex may also select the skill from its description when an EmberBSD task
matches. The installed host controls skill selection and available tools.

Additional starting prompts:

> Update this EmberBSD port to the current stable release. Use
> $emberbsd-repository-guide, inspect pkgsrc and pkgsrc-wip, fix compatibility,
> and test the package and a runtime scenario before opening the contribution.

> Use $emberbsd-repository-guide to turn this reproduced build failure into a
> tested fix, prepare the EmberBSD and upstream submissions, and update the
> affected developer instructions.

The workflow records original sources and SHA256, keeps a coherent toolchain,
and requires real test evidence before a ready PR. Upstream submission follows
the target project's actual channel and AI-assistance rules.

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

For another development assistant, load `SKILL.md` together with its bundled
references using that client's documented skill mechanism. Only Codex discovery
is currently verified; this repository does not claim tested Cursor or Claude
Code installation. Keep relative reference paths intact.

## License

[MIT](LICENSE).
