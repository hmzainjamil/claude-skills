# Git Worktree Manager

CLI helpers for creating Git worktrees, assigning suggested ports from existing worktree metadata, copying selected environment files, and inspecting stale worktrees. Port assignments are not checked against all processes on the host.

## Quick Start

```bash
# Create + prepare a worktree
python scripts/worktree_manager.py \
  --repo . \
  --branch feature/api-hardening \
  --name wt-api-hardening \
  --base-branch main \
  --install-deps \
  --format text

# Review stale worktrees
python scripts/worktree_cleanup.py --repo . --stale-days 14 --format text
```

## Included Tools

- `scripts/worktree_manager.py`: create/prep workflow; ports are chosen from `.worktree-ports.json` files in listed worktrees; copies `.env`, `.env.local`, `.env.development`, and `.envrc` as-is; optional install runs detected package-manager commands
- `scripts/worktree_cleanup.py`: stale/dirty/merged analysis; `--remove-merged` removes stale, clean, merged worktrees, while `--force` also permits removal of dirty worktrees

Both support `--input <json-file>` and stdin JSON for automation. The manager may copy secrets from those environment files and may run package installation commands. Review files and commands before enabling it. Cleanup is non-removing by default; `--remove-merged --force` can delete dirty worktree contents.

## References

- `references/port-allocation-strategy.md`
- `references/docker-compose-patterns.md`

## Installation

### Claude Code

```bash
cp -R engineering/git-worktree-manager ~/.claude/skills/git-worktree-manager
```

### OpenAI Codex

```bash
cp -R engineering/git-worktree-manager ~/.codex/skills/git-worktree-manager
```

### OpenClaw

```bash
cp -R engineering/git-worktree-manager ~/.openclaw/skills/git-worktree-manager
```
