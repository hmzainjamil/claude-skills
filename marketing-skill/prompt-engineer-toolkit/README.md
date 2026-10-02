# Prompt Engineer Toolkit

Scripts for heuristic prompt scoring and local prompt version history. The scoring is not a validated quality or model benchmark.

## Quick Start

```bash
# Score prompts against supplied cases
python3 scripts/prompt_tester.py \
  --prompt-a-file prompts/a.txt \
  --prompt-b-file prompts/b.txt \
  --cases-file testcases.json \
  --format text
```

Without `--runner-cmd`, the tester runs in static mode: it substitutes `{{input}}` into prompt text and scores that text against the case string/regex checks. It does not call a model. To evaluate model outputs, supply a project-specific external runner with `--runner-cmd`; review the runner and case criteria. The reported winner is only the higher heuristic score, not a statistically validated result.

```bash
# Store a prompt version
python3 scripts/prompt_versioner.py add \
  --name support_classifier \
  --prompt-file prompts/a.txt \
  --author team
```

## Included Tools

- `scripts/prompt_tester.py`: Compares two prompts using case-level expected/forbidden strings and regexes; static mode by default, optional caller-supplied command runner
- `scripts/prompt_versioner.py`: Prompt history (`add`, `list`, `diff`, `changelog`) in a local JSONL store

## References

- `references/prompt-templates.md`
- `references/technique-guide.md`
- `references/evaluation-rubric.md`

## Installation

### Claude Code

```bash
cp -R marketing-skill/prompt-engineer-toolkit ~/.claude/skills/prompt-engineer-toolkit
```

### OpenAI Codex

```bash
cp -R marketing-skill/prompt-engineer-toolkit ~/.codex/skills/prompt-engineer-toolkit
```

### OpenClaw

```bash
cp -R marketing-skill/prompt-engineer-toolkit ~/.openclaw/skills/prompt-engineer-toolkit
```
