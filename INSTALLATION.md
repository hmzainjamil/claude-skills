# Installation guide

This repository stores agent skills and supporting files. It has no root npm package or application service. Choose one host workflow and inspect its installer before changing user directories.

The upstream project is identified in the plugin metadata as [alirezarezvani/claude-skills](https://github.com/alirezarezvani/claude-skills), authored by Alireza Rezvani. The local marketplace metadata points to that upstream repository. Follow that source if you intend to install the upstream marketplace release.

## Get the repository

```sh
git clone https://github.com/hmzainjamil/claude-skills.git
cd claude-skills
```

Check the selected install script before running it. Current tree and documentation indexes disagree on skill totals, and host export directories may contain copies.

## Codex

The Codex installer reads the local `.codex/skills/` export and targets `~/.codex/skills` by default. It can list available skills, preview changes, or install all/specific content.

```sh
./scripts/codex-install.sh --list
./scripts/codex-install.sh --dry-run
./scripts/codex-install.sh
```

Use `--category <name>` or `--skill <name>` to narrow an install. Set `CODEX_SKILLS_DIR` to choose another destination. The installer writes into that directory; review existing names and files before confirming an overwrite.

## Gemini CLI

The repository includes a synchronization script and an index under `.gemini/`.

```sh
./scripts/gemini-install.sh --dry-run
./scripts/gemini-install.sh
```

The setup script requires Python 3 and invokes `scripts/sync-gemini-skills.py`. Review that script's target paths before running it. It changes the repository's Gemini export/index files; do not assume it installs content into a user-wide location.

## OpenClaw

The installer supports a dry run:

```sh
./scripts/openclaw-install.sh --dry-run
./scripts/openclaw-install.sh
```

The current script scans recursively for every `SKILL.md` in this repository and creates symlinks under `~/.openclaw/workspace/skills`. That scan includes host-export copies and can encounter duplicate skill names. Inspect the dry-run output and target directory before installing.

## Other conversion targets

`scripts/convert.sh` and `scripts/install.sh` support conversion/install workflows for Antigravity, Cursor, Aider, Kilo Code, Windsurf, OpenCode, and Augment. The installer expects generated directories under `integrations/<tool>/`; these are not part of the checked-in tree by default.

Inspect available options and generated paths first:

```sh
./scripts/convert.sh --help
./scripts/install.sh --help
```

Then preview conversion or installation using the script's documented options. `scripts/install.sh` accepts `--target` and `--force`; without a target, several targets write to the current working directory. Review that behavior before continuing.

## Claude Code plugin metadata

The repository contains `.claude-plugin/marketplace.json`, but its repository and homepage fields point to the upstream Alireza Rezvani project. Do not assume a marketplace command against this checkout installs the current `hmzainjamil` repository. For local installation, verify the host's current plugin documentation and the metadata source before proceeding.

## Verification

The repository has scripts for synchronization and conversion. Use `--list` or `--dry-run` where available, then confirm the resulting files and target directory. This guide update did not run an installer, conversion, sync, build, or test.
