# dsh-plugin-mattpocock-skills

Turns [mattpocock/skills][upstream] into a dsh plugin.

**English** | [简体中文](README-zh.md)

## What this is

A DeepSeek Harness plugin that adds every skill from
[mattpocock/skills][upstream] to your session catalog. Nothing is copied into
`~/.agents/skills`, and skills upstream marks `disable-model-invocation` stay
reachable only by `/name`, never by the model.

| | |
|---|---|
| Upstream | [github.com/mattpocock/skills][upstream] (MIT), synced daily |
| DSH | `>=0.2.0-rc.1 <0.3.0-0` |
| Runtime deps | none |

## Who needs this

**You already installed Matt Pocock's skills as a Codex plugin, and you do not
want a second copy in `~/.agents/skills` just so DSH can see them.**

Codex keeps its skills inside its own storage, which a Harness session never
reads. Harness only discovers skills under `<project>/.dsh/skills`,
`<project>/.agents/skills`, `~/.dsh/skills`, and `~/.agents/skills`. Copying the
skills into one of those works, but it leaves two copies with two update paths
that drift apart. This plugin is the alternative: DSH gets the skills without a
second copy.

**Not needed** if the skills already sit in `~/.agents/skills` or
`<project>/.agents/skills`: those locations take precedence, so this plugin would
be shadowed and the two copies would disagree. Pick one.

## Usage

```bash
dsh plugin --profile <profile> add dsh-plugin-mattpocock-skills
```

Then enable the bundle once — Web UI **Plugins → Bundles**, or add it to
`dsh.profile.bundles` — and restart the Harness. Every skill now appears in the
session catalog, reachable with the `skill` tool or as `/name`.

To install from a checkout instead, pass its path instead of the package name:

```bash
dsh plugin --profile <profile> add /absolute/path/to/dsh-plugin-mattpocock-skills
dsh plugin --profile <profile> remove dsh-plugin-mattpocock-skills   # uninstall
```

---

Plugin code is MIT. The skills are MIT, © Matt Pocock, with the upstream licence
at `skills/LICENSE`; see [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md).

Maintaining this package — syncing upstream, verification, releases — is
automated; see `scripts/` and [`.github/workflows/release.yml`](.github/workflows/release.yml).

[upstream]: https://github.com/mattpocock/skills
