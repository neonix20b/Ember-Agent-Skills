# Codex client adapter

The [portable package](packaging.md) uses Agent Plugins and Agent Skills.
This page documents the Codex adapter and its checks. Other clients use their
own installation, update and invocation mechanisms.

## Install and refresh

Use a Codex CLI that provides `codex plugin marketplace` and `codex plugin add`:

```sh
codex plugin marketplace add oxtech-ember/Ember-Agent-Skills --ref main
codex plugin list --marketplace ember-agent-skills --available --json
codex plugin add emberbsd-development@ember-agent-skills
```

The first command registers the Git catalog, the second lists its packages,
and the third installs the chosen plugin. The listing should include
`emberbsd-development@ember-agent-skills` at version `0.3.3`. Start a new
conversation and select `$emberbsd-repository-guide`. In the desktop app,
check the Plugins view for the installed package.

| Identifier | Meaning |
| --- | --- |
| `Ember-Agent-Skills` | Source repository |
| `ember-agent-skills` | Codex marketplace name |
| `emberbsd-development` | Portable plugin name |
| `emberbsd-development@ember-agent-skills` | Codex installation identifier |

To refresh the Git catalog:

```sh
codex plugin marketplace upgrade ember-agent-skills
```

The catalog snapshot and installed plugin can be separate. Check the installed
version and reinstall if it still shows an old copy; start a new conversation
for the refreshed skill. If a command is unavailable, inspect `codex --version`
and `codex plugin --help`. A clone alone does not install the package in an
unrelated application project.

## Metadata

The catalog at `.agents/plugins/marketplace.json` points to `./`, relative to
the marketplace root. Its entry identifies `emberbsd-development`. The policy
allows installation; this skills-only package needs no account authentication.

`extensions.com.openai` in root `plugin.json` supplies the display metadata.
There is no duplicate `.codex-plugin/plugin.json` overlay. Inline OpenAI
metadata replaces that entire compatibility overlay when present, as described
in the [official packaging guide](https://developers.openai.com/plugins/build/plugins).
The skill's `agents/openai.yaml` adds display text and a suggested prompt.
These files do not replace the portable manifest or `SKILL.md`.

## What was checked

Native discovery passed with **Codex CLI 0.162.0-alpha.2** on **2026-10-08**
for package **0.3.3**. Earlier package versions were checked with CLI 0.160.1.
The command syntax was also inspected with the local CLI's help.

```sh
ruby scripts/check-package.rb --codex
```

The check supplies a temporary profile and a local marketplace through a `-c`
override, then verifies the discovered plugin ID and release. This prevents an
installed older release from hiding the candidate in the available list. It
does not register a source, install or update the user's plugin, or execute
the skill. See the portable
[manual acceptance scenarios](packaging.md#checks-and-evidence) for behavior
that package discovery cannot establish.

Git distribution is separate from OpenAI's public directory. This repository
has not been submitted there. Any future submission must follow the current
[submission process](https://developers.openai.com/plugins/deploy/submission).
