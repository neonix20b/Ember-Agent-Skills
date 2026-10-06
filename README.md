# Ember Agent Skills

Developer skills for [EmberBSD](https://github.com/apovalixin/EmberBSD), packaged
as an installable Codex plugin and a Git-backed plugin marketplace.

The initial version, **0.1.0**, includes one skill:

| Skill | Purpose |
| --- | --- |
| [`emberbsd-repository-guide`](skills/emberbsd-repository-guide/SKILL.md) | Identify the owning repository, inspect available interfaces, and distinguish source, build, VM, and hardware evidence |

This version provides repository guidance. SDK scaffolding, Wasm packaging,
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

## License

[MIT](LICENSE).
