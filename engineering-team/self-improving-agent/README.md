# Self-Improving Agent

> Auto-memory may capture. These prompt-driven workflows help curate.

A Claude Code plugin that provides prompt-driven workflows for reviewing auto-memory, proposing durable rules, and drafting reusable skills. Review and approve every proposed change.

## Why

When Claude Code auto-memory is available and enabled, it can record project patterns in `MEMORY.md`. These workflow prompts help review those notes; they do not run a background memory service or independently verify patterns.

**The difference:**
- **MEMORY.md**: "I noticed this project uses pnpm" (background note, truncated at 200 lines)
- **CLAUDE.md**: "Use pnpm, not npm" (enforced instruction, loaded in full)

Promoting a pattern from memory to rules fundamentally changes how Claude treats it.

## Commands

| Command | What it does |
|---------|-------------|
| `/si:review` | Analyze auto-memory — find promotion candidates, stale entries, health metrics |
| `/si:promote` | Graduate a pattern from MEMORY.md → CLAUDE.md or `.claude/rules/` |
| `/si:extract` | Turn a recurring pattern into a standalone reusable skill |
| `/si:status` | Memory health dashboard — line counts, capacity, recommendations |
| `/si:remember` | Explicitly save important knowledge to auto-memory |

## Install

### Claude Code
```
/plugin marketplace add alirezarezvani/claude-skills
/plugin install self-improving-agent@claude-code-skills
```

### OpenClaw
```bash
clawhub install self-improving-agent
```

### Codex CLI
```bash
./scripts/codex-install.sh --skill self-improving-agent
```

## How It Works

```
Claude discovers pattern → auto-memory (MEMORY.md)
         ↓
Pattern recurs 2-3x → /si:review flags it
         ↓
You approve → /si:promote graduates it to CLAUDE.md
         ↓
Pattern becomes enforced rule, memory entry removed
         ↓
Space freed for new learnings
```

## What's Included

| Component | Count | Description |
|-----------|-------|-------------|
| Skills | 5 | review, promote, extract, status, remember |
| Agents | 2 | memory-analyst, skill-extractor |
| Hooks | 1 | PostToolUse Bash-output scanner that emits an error reminder when fixed patterns match |
| Reference docs | 3 | memory architecture, promotion rules, rules directory patterns |
| Templates | 2 | rule template, skill template |

## Design Principles

1. **Work with host memory.** When host auto-memory is available, review and curate its entries through explicit prompts.
2. **No separate database included.** The workflows target host memory and instruction files; users review and confirm changes.
3. **Error reminder hook.** The hook runs after Bash calls, scans output against fixed patterns, and emits a reminder on matches. It does not save to memory; false positives and missed errors are possible.
4. **Promotion = graduation.** Moving a pattern from MEMORY.md to CLAUDE.md changes its priority.
5. **Check host limits.** Memory capacity behavior can vary by host version and settings.

## Platform Support

These entries describe intended adaptations and install paths; they do not prove equivalent command or hook behavior across host versions. Verify the host-specific setup before relying on an integration.

| Platform | Memory System | Support |
|----------|--------------|---------|
| Claude Code | Auto-memory (MEMORY.md) | ✅ Full |
| OpenClaw | workspace/MEMORY.md | ✅ Adapted |
| Codex CLI | AGENTS.md | ✅ Adapted |
| GitHub Copilot | copilot-instructions.md | ⚠️ Manual |

## Credits

Inspired by [pskoett/self-improving-agent](https://clawhub.ai/pskoett/self-improving-agent) — a structured learning loop for AI coding agents. This plugin builds on that concept by integrating natively with Claude Code's auto-memory system.

## License

MIT — see [LICENSE](LICENSE)
