# Code → PRD

Static analysis tools that extract selected routes, API references, and project signals, then scaffold a PRD draft. They do not generate a complete or validated PRD; review extracted data and fill the marked sections.

## Quick Start

```bash
# One command
/code-to-prd /path/to/project

# Or step by step
python3 scripts/codebase_analyzer.py /path/to/project -o analysis.json
python3 scripts/prd_scaffolder.py analysis.json -o prd/ -n "My App"
```

## Supported Frameworks

The analyzer uses file and text patterns for these stacks; coverage is partial and may miss routes or APIs that do not match its patterns.

| Stack | Frameworks |
|-------|-----------|
| Frontend | React, Vue, Angular, Svelte, Next.js, Nuxt, SvelteKit, Remix |
| Backend | NestJS, Express, Django, DRF, FastAPI, Flask |
| Fullstack | Next.js (pages + API), Nuxt (pages + server), Django (views + templates) |

## What It Generates

The scaffolder creates a PRD skeleton populated with signals found by the analyzer. Sections marked TODO require human completion.

```text
prd/
├── README.md                  # System overview
├── pages/
│   ├── 01-user-mgmt-list.md   # Per-page/endpoint docs
│   └── ...
└── appendix/
    ├── enum-dictionary.md      # All enums and status codes
    ├── api-inventory.md        # Complete API reference
    └── page-relationships.md   # Navigation and data coupling
```

## Scripts

| Script | Purpose |
|--------|---------|
| `codebase_analyzer.py` | Scan supported source files with heuristics and output selected routes, APIs, models, and signals |
| `prd_scaffolder.py` | Generate a PRD directory skeleton and TODO placeholders from analysis JSON |

Both scripts use the Python standard library. Run `--help` for usage.

## References

- `references/framework-patterns.md` — Route, state, API, form, and model patterns per framework
- `references/prd-quality-checklist.md` — Validation checklist for completeness and accuracy

## Attribution

Inspired by [code-to-prd](https://github.com/lihanglogan/code-to-prd) by [@lihanglogan](https://github.com/lihanglogan).

## License

MIT
