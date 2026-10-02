# Claude Skills Library

A repository of reusable agent skills, supporting scripts, references, and host-specific exports. Skills are instruction files and related resources; this repository is not itself a running agent service.

The plugin manifests identify [Alireza Rezvani](https://github.com/alirezarezvani) as author and [alirezarezvani/claude-skills](https://github.com/alirezarezvani/claude-skills) as the upstream project. Preserve that attribution and the [MIT license](./LICENSE).

## At a glance

| Field | Details |
|---|---|
| Main content | Skills, reference files, scripts, agents, and commands |
| Source domains | Engineering, marketing, product, leadership, finance, project management, business growth, and regulatory/quality |
| Host exports | Claude Code, Codex, Gemini CLI, OpenClaw, and conversion targets |
| Install guidance | [INSTALLATION.md](./INSTALLATION.md) |
| Authoring rules | [SKILL-AUTHORING-STANDARD.md](./SKILL-AUTHORING-STANDARD.md), [CONVENTIONS.md](./CONVENTIONS.md) |
| License | MIT; see [LICENSE](./LICENSE) |

At the 2026-10-02 repository snapshot, the tree contained 540 `SKILL.md` paths: 239 outside host export directories and 301 under `.gemini/`. These are file paths, not a unique-skill count; some are copied host exports. The README, plugin manifests, host indexes, and documentation report different totals. Regenerate or inspect the current tree before publishing a count.

## Install a host export

For Codex, inspect the available skills and preview the installer before it writes to your user directory:

```sh
./scripts/codex-install.sh --list
./scripts/codex-install.sh --dry-run
```

To install, run `./scripts/codex-install.sh`. The script targets `~/.codex/skills` by default. Review [INSTALLATION.md](./INSTALLATION.md) for Gemini, OpenClaw, and conversion scripts, including their filesystem effects.

## Repository map

| Path | Purpose |
|---|---|
| Domain directories such as `engineering/` and `marketing-skill/` | Skill source files and supporting assets |
| `.claude-plugin/` | Claude Code marketplace metadata |
| `.codex-plugin/`, `.codex/` | Codex plugin metadata and generated skill export |
| `.gemini/` | Gemini CLI metadata and generated skill export |
| `agents/`, `commands/` | Agent/persona and command guidance |
| `scripts/` | Installers, conversion, synchronization, and documentation tools |
| `docs/`, `documentation/` | Guides and generated reference pages |
| `tests/`, `eval-workspace/` | Test and evaluation material |

There is no root `package.json` or `.env.example`. Do not use npm package commands or invent environment settings for this repository.

## Safety and limitations

Skills can instruct an agent to use tools or run bundled scripts. Read a skill, its references, and any scripts before enabling it. Installer scripts copy or link content into user directories; use their dry-run options where available and check the target path first.

Host exports, skill indexes, and install documentation are generated or maintained separately and can drift. Compatibility also depends on the host application's current skill-discovery rules. Presence in this repository does not prove a skill was tested, installed, or safe for a particular environment.

## Documentation

- [Installation guide](./INSTALLATION.md)
- [Skill authoring standard](./SKILL-AUTHORING-STANDARD.md)
- [Repository conventions](./CONVENTIONS.md)
- [Skill production pipeline](./SKILL_PIPELINE.md)
- [Documentation site index](./docs/index.md)
- [Contribution guide](./CONTRIBUTING.md)

No install, conversion, build, or test command was run for this README update.
