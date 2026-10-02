---
title: Claude Skills Library Documentation
description: "Guides and reference pages for the Claude Skills Library repository."
hide:
  - toc
  - edit
---

# Claude Skills Library

This repository contains reusable skill instructions, scripts, references, agents, and host-specific exports. It is a content library, not a running agent service. Read the [root README](https://github.com/hmzainjamil/claude-skills#readme) for current scope and provenance.

The upstream author and repository are identified in the plugin metadata as [Alireza Rezvani](https://github.com/alirezarezvani) and [alirezarezvani/claude-skills](https://github.com/alirezarezvani/claude-skills). Preserve that attribution.

## Start here

- [Installation guide](https://github.com/hmzainjamil/claude-skills/blob/main/INSTALLATION.md): host-specific installers and their filesystem effects.
- [Browse skill domains](skills/index.md): source directories and generated host exports.
- [Agent and persona index](agents/index.md)
- [Command index](commands/index.md)
- [Plugin index](plugins/index.md)

## Authoring and repository guidance

- [Skill authoring standard](https://github.com/hmzainjamil/claude-skills/blob/main/SKILL-AUTHORING-STANDARD.md)
- [Repository conventions](https://github.com/hmzainjamil/claude-skills/blob/main/CONVENTIONS.md)
- [Skill production pipeline](https://github.com/hmzainjamil/claude-skills/blob/main/SKILL_PIPELINE.md)
- [Contribution guide](https://github.com/hmzainjamil/claude-skills/blob/main/CONTRIBUTING.md)

## Inventory note

The README, plugin manifests, host indexes, and documentation contain different skill totals. File counts include duplicate host exports and do not establish the number of unique skills. Verify the current repository tree before publishing inventory numbers.

Compatibility depends on each host's current discovery rules. Review a skill and its scripts before installing or enabling it.
