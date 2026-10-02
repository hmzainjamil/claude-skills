# Tech Debt Tracker

A set of Python scripts that flag selected code patterns, rank supplied debt records with fixed formulas, and summarize historical inventories. Outputs are heuristic signals for human review, not a complete code, security, dependency, or business-impact audit.

## Overview

**Scope limits:** Scanner findings are pattern-based, Python receives AST checks, and non-Python checks are general text/regex rules. The prioritizer and dashboard use built-in formulas and provided inventories; their scores are not verified business ROI or observed productivity metrics. Review every result before acting.

Technical debt can affect maintenance and delivery, but its cost varies by project. These scripts provide:

- **Pattern-Based Scanning**: Flag selected code patterns using Python AST checks and general text/regex rules
- **Heuristic Prioritization**: Apply named WSJF/RICE/Cost-of-Delay-style formulas to inventory fields and fixed weights
- **Inventory Summaries**: Compare supplied snapshots and report formula-derived scores and trends

## Tools

### 1. Debt Scanner (`debt_scanner.py`)

Flags selected technical-debt signals using AST parsing for Python and general text/regex patterns for other supported file extensions. This is not a full parser or security scanner.

**Features:**
- Flags selected signals such as long functions, complexity patterns, duplicate text blocks, TODOs, and a few regex-based code smells
- Python structure checks plus general text/regex checks for configured extensions (JavaScript, Java, C#, Go, Ruby, PHP, Rust, Kotlin, and C/C++)
- Configurable thresholds and rules
- Dual output: JSON for tools, human-readable for reports

**Usage:**
```bash
# Basic scan
python scripts/debt_scanner.py /path/to/codebase

# With custom config and output
python scripts/debt_scanner.py /path/to/codebase --config config.json --output report.json

# Different output formats
python scripts/debt_scanner.py /path/to/codebase --format both
```

### 2. Debt Prioritizer (`debt_prioritizer.py`)

Ranks a supplied debt inventory using selectable weighted formulas labeled Cost of Delay, WSJF, or RICE. Scores depend on the input fields and configured assumptions; they are not measured ROI.

**Features:**
- Formula variants labeled Cost of Delay, WSJF, and RICE
- Rule-based business-impact estimates from debt type and inventory fields; no empirical ROI calculation  
- Sprint allocation recommendations
- Effort estimation with risk adjustment
- Executive and engineering reports

**Usage:**
```bash
# Basic prioritization
python scripts/debt_prioritizer.py debt_inventory.json

# Custom framework and team size
python scripts/debt_prioritizer.py inventory.json --framework wsjf --team-size 8

# Sprint capacity planning
python scripts/debt_prioritizer.py inventory.json --sprint-capacity 80 --output backlog.json
```

### 3. Debt Dashboard (`debt_dashboard.py`)

Summarizes supplied scan snapshots with formula-derived health, velocity, and trend metrics; it does not measure team velocity or render an interactive dashboard.

**Features:**
- Health score trending over time
- Debt velocity analysis (accumulation vs resolution)
- Summary fields and heuristic impact estimates
- Simple trend-based projections from supplied snapshots
- Strategic recommendations

**Usage:**
```bash
# Single directory of scans
python scripts/debt_dashboard.py --input-dir ./debt_scans/

# Multiple specific files
python scripts/debt_dashboard.py scan1.json scan2.json scan3.json

# Custom analysis period
python scripts/debt_dashboard.py data.json --period quarterly --team-size 6
```

## Quick Start

### 1. Scan Your Codebase

```bash
# Scan your project
python scripts/debt_scanner.py ~/my-project --output initial_scan.json

# Review the results
python scripts/debt_scanner.py ~/my-project --format text
```

### 2. Prioritize Your Debt

```bash
# Create prioritized backlog
python scripts/debt_prioritizer.py initial_scan.json --output backlog.json

# View sprint recommendations
python scripts/debt_prioritizer.py initial_scan.json --format text
```

### 3. Track Over Time

```bash
# After multiple scans, analyze trends
python scripts/debt_dashboard.py scan1.json scan2.json scan3.json --output dashboard.json

# Generate executive report
python scripts/debt_dashboard.py --input-dir ./scans/ --format text
```

## Configuration

### Scanner Configuration

Create `config.json` to customize detection rules:

```json
{
  "max_function_length": 50,
  "max_complexity": 10,
  "max_nesting_depth": 4,
  "ignore_patterns": ["*.test.js", "build/", "node_modules/"],
  "file_extensions": {
    "python": [".py"],
    "javascript": [".js", ".jsx", ".ts", ".tsx"]
  }
}
```

### Team Configuration

Adjust tools for your team size and sprint capacity:

```bash
# 8-person team with 2-week sprints
python scripts/debt_prioritizer.py inventory.json --team-size 8 --sprint-capacity 160
```

## Sample Data

The `assets/` directory contains sample data for testing:

- `sample_codebase/`: Example codebase with various debt types
- `sample_debt_inventory.json`: Example debt inventory
- `historical_debt_*.json`: Sample historical data for trending

Try the tools on sample data:

```bash
# Test scanner
python scripts/debt_scanner.py assets/sample_codebase

# Test prioritizer  
python scripts/debt_prioritizer.py assets/sample_debt_inventory.json

# Test dashboard
python scripts/debt_dashboard.py assets/historical_debt_*.json
```

## Understanding the Output

### Health Score (0-100)

- **85-100**: Excellent - Minimal debt, sustainable practices
- **70-84**: Good - Manageable debt level, some attention needed
- **55-69**: Fair - Debt accumulating, requires focused effort
- **40-54**: Poor - High debt level, impacts productivity
- **0-39**: Critical - Immediate action required

### Priority Levels

- **Critical**: Security issues, blocking problems (fix immediately)
- **High**: Significant impact on quality or velocity (next sprint)
- **Medium**: Moderate impact, plan for upcoming work (next quarter)
- **Low**: Minor issues, fix opportunistically (when convenient)

### Debt Categories

- **Code Quality**: Large functions, complexity, duplicates
- **Architecture**: Design issues, coupling problems
- **Security**: Vulnerabilities, hardcoded secrets
- **Testing**: Missing tests, poor coverage
- **Documentation**: Missing or outdated docs
- **Dependencies**: Outdated packages, license issues

## Integration with Development Workflow

### CI/CD Integration

Add debt scanning to your CI pipeline:

```bash
# In your CI script
python scripts/debt_scanner.py . --output ci_scan.json
# Compare with baseline, fail build if critical issues found
```

### Sprint Planning

1. **Weekly**: Run scanner to detect new debt
2. **Sprint Planning**: Use prioritizer for debt story sizing
3. **Monthly**: Generate dashboard for trend analysis
4. **Quarterly**: Executive review with strategic recommendations

### Code Review Integration

Use scanner output to focus code reviews:

```bash
# Scan PR branch
python scripts/debt_scanner.py . --output pr_scan.json

# Compare with main branch baseline
# Focus review on areas with new debt
```

## Best Practices

### Debt Management Strategy

1. **Prevention**: Use scanner in CI to catch debt early
2. **Prioritization**: Always use business impact for priority
3. **Allocation**: Reserve 15-20% sprint capacity for debt work
4. **Measurement**: Track health score and velocity impact
5. **Communication**: Use dashboard reports for stakeholders

### Common Pitfalls to Avoid

- **Analysis Paralysis**: Don't spend too long on perfect prioritization
- **Technical Focus Only**: Always consider business impact
- **Inconsistent Application**: Ensure all teams use same approach
- **Ignoring Trends**: Pay attention to debt accumulation rate
- **All-or-Nothing**: Incremental debt reduction is better than none

### Success Metrics

- **Health Score Improvement**: Target 5+ point quarterly improvement
- **Velocity Impact**: Keep debt velocity impact below 20%
- **Team Satisfaction**: Survey developers on code quality satisfaction
- **Incident Reduction**: Track correlation between debt and production issues

## Advanced Usage

### Custom Debt Types

Extend the scanner for organization-specific debt patterns:

1. Add patterns to `config.json`
2. Modify detection logic in scanner
3. Update categorization in prioritizer

### Integration with External Tools

- **Jira/GitHub**: Import debt items as tickets
- **SonarQube**: Combine with static analysis metrics
- **APM Tools**: Correlate debt with performance metrics
- **Chat Systems**: Send debt alerts to team channels

### Automated Reporting

Set up automated debt reporting:

```bash
#!/bin/bash
# Daily debt monitoring script
python scripts/debt_scanner.py . --output daily_scan.json
python scripts/debt_dashboard.py daily_scan.json --output daily_report.json
# Send report to stakeholders
```

## Troubleshooting

### Common Issues

**Scanner not finding files**: Check `ignore_patterns` in config
**Prioritizer giving unexpected results**: Verify business impact scoring
**Dashboard shows flat trends**: Need more historical data points

### Performance Tips

- Use `.gitignore` patterns to exclude irrelevant files
- Limit scan depth for large monorepos
- Run dashboard analysis on subset for faster iteration

### Getting Help

1. Check the `references/` directory for detailed documentation
2. Review sample data and expected outputs
3. Examine the tool source code for customization ideas

## Contributing

This skill is designed to be customized for your organization's needs:

1. **Add Detection Rules**: Extend scanner patterns for your tech stack
2. **Custom Prioritization**: Modify scoring algorithms for your business context
3. **New Report Formats**: Add output formats for your stakeholders
4. **Integration Hooks**: Add connectors to your existing tools

The codebase is designed with extensibility in mind - each tool is modular and can be enhanced independently.

---

**Remember**: Technical debt management is a journey, not a destination. These tools help you make informed decisions about balancing new feature development with technical excellence. Start small, measure impact, and iterate based on what works for your team.