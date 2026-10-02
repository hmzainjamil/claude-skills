# A11y Audit — WCAG 2.2 Accessibility Audit & Fix

Run static checks for selected accessibility patterns in HTML, JSX/TSX, Vue, Svelte, and CSS used by frontend projects. Findings need manual and browser-based review; this is not a complete WCAG audit or proof of compliance.

## Quick Start

```bash
# Scan a project
/a11y-audit ./src

# Or use the scripts directly
python3 scripts/a11y_scanner.py ./src
python3 scripts/contrast_checker.py "#1a1a2e" "#ffffff"
```

## Scripts

| Script | Purpose |
|--------|---------|
| `a11y_scanner.py` | Scan supported source files for selected rule-based accessibility findings |
| `contrast_checker.py` | WCAG contrast ratio calculator with AA/AAA checks and `--suggest` mode |

Both are stdlib-only — no pip install needed. Exit codes differ: scanner returns 1 for critical/serious findings, 2 for moderate/minor findings, and 0 otherwise; contrast checker returns 0 when the AA normal-text ratio passes and 1 when it fails or input is invalid. A zero scanner exit does not mean no findings or WCAG compliance.

## What It Covers

- **Images**: missing alt, empty alt on informative images
- **Forms**: missing labels, orphan labels, missing fieldset/legend
- **Headings**: skipped levels, missing h1, multiple h1s
- **Landmarks**: missing main/nav/skip link
- **Keyboard**: tabindex > 0, click without keyboard handler
- **ARIA**: invalid attributes, aria-hidden on focusable, missing aria-live
- **Color**: contrast ratios below AA thresholds
- **Links**: empty links, "click here" text
- **Tables**: missing headers, missing caption
- **Media**: missing captions, autoplay without controls

## References

- `references/wcag-quick-ref.md` — WCAG 2.2 Level A/AA criteria table
- `references/aria-patterns.md` — ARIA roles, live regions, keyboard patterns
- `references/framework-a11y-patterns.md` — React, Vue, Angular, Svelte fix patterns

## License

MIT
