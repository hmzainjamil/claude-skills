# Skill Tester - Quality Assurance Meta-Skill

A POWERFUL-tier skill that provides comprehensive validation, testing, and quality scoring for skills in the claude-skills ecosystem.

## Overview

The Skill Tester is a meta-skill that ensures quality and consistency across all skills in the repository through:

- **Structure Validation** - Verifies directory structure, file presence, and documentation standards
- **Script Testing** - Tests Python scripts for syntax, functionality, and compliance
- **Quality Scoring** - Provides comprehensive quality assessment across multiple dimensions

## Quick Start

### Validate a Skill
```bash
# Basic validation
python3 engineering/skill-tester/scripts/skill_validator.py engineering/my-skill

# Validate against specific tier
python scripts/skill_validator.py engineering/my-skill --tier POWERFUL --json
```

### Test Scripts
```bash
# Test all scripts in a skill
python3 engineering/skill-tester/scripts/script_tester.py engineering/my-skill

# Test with custom timeout
python scripts/script_tester.py engineering/my-skill --timeout 60 --json
```

### Score Quality
```bash
# Get quality assessment
python3 engineering/skill-tester/scripts/quality_scorer.py engineering/my-skill

# Detailed scoring with improvement suggestions
python scripts/quality_scorer.py engineering/my-skill --detailed --json
```

## Components

### Scripts
- **skill_validator.py** (667 lines) - Validates skill structure and compliance
- **script_tester.py** (730 lines) - Tests script functionality and quality
- **quality_scorer.py** (1,181 lines) - Scores skills across quality dimensions
- **security_scorer.py** (605 lines) - Optional security scoring module used by `quality_scorer.py`

### Reference Documentation
- **skill-structure-specification.md** - Complete structural requirements
- **tier-requirements-matrix.md** - Tier-specific quality standards
- **quality-scoring-rubric.md** - Detailed scoring methodology

### Sample Assets
- **sample-skill/** - Complete sample skill for testing the tester itself

## Features

### Validation Capabilities
- SKILL.md format and content validation
- Directory structure compliance checking
- Python script syntax and import validation
- Argparse implementation verification
- Tier-specific requirement enforcement

### Testing Framework
- Syntax validation using AST parsing
- Import analysis for external dependencies
- Runtime execution testing with timeout protection
- Help functionality verification
- Sample data processing validation
- Output format compliance checking

### Quality Assessment
- Default scoring: documentation, code quality, completeness, and usability at 25% each
- Optional security scoring with `--include-security`: five dimensions at 20% each
- Letter grade assignment (A+ to F)
- Tier recommendation generation
- Improvement roadmap creation

## CI/CD Integration

### GitHub Actions Example
```yaml
name: Skill Quality Gate
on:
  pull_request:
    paths: ['engineering/**']
    
jobs:
  validate-skills:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Setup Python
        uses: actions/setup-python@v4
        with:
          python-version: '3.11'
      - name: Validate Skills
        run: |
          for skill in $(git diff --name-only ${{ github.event.before }} | grep -E '^engineering/[^/]+/' | cut -d'/' -f1-2 | sort -u); do
            python engineering/skill-tester/scripts/skill_validator.py $skill --json
            python engineering/skill-tester/scripts/script_tester.py $skill
            python engineering/skill-tester/scripts/quality_scorer.py $skill --minimum-score 75
          done
```

### Pre-commit Hook
```bash
#!/bin/bash
# .git/hooks/pre-commit
python engineering/skill-tester/scripts/skill_validator.py engineering/my-skill --tier STANDARD
if [ $? -ne 0 ]; then
    echo "Skill validation failed. Commit blocked."
    exit 1
fi
```

## Quality Standards

### All Scripts
- **Zero External Dependencies** - Python standard library only
- **Comprehensive Error Handling** - Meaningful error messages and recovery
- **Dual Output Support** - Both JSON and human-readable formats
- **Proper Documentation** - Comprehensive docstrings and comments
- **CLI Best Practices** - Full argparse implementation with help text

### Validation Accuracy
- **Structure Checks** - Checks required directories and files against configured rules
- **Content Analysis** - Parses SKILL.md and documentation using defined checks
- **Code Analysis** - Uses AST-based Python code validation
- **Compliance Scoring** - Applies documented scoring rules; results are guidance, not a guarantee of correctness

## Self-Testing

The skill-tester can validate itself:

```bash
# Validate the skill-tester structure
python3 engineering/skill-tester/scripts/skill_validator.py engineering/skill-tester --tier POWERFUL

# Test the skill-tester scripts
python3 engineering/skill-tester/scripts/script_tester.py engineering/skill-tester

# Score the skill-tester quality
python3 engineering/skill-tester/scripts/quality_scorer.py engineering/skill-tester --detailed
```

## Advanced Usage

### Batch Validation
```bash
# Validate all skills in repository
find engineering/ -maxdepth 1 -type d | while read skill; do
  echo "Validating $skill..."
  python engineering/skill-tester/scripts/skill_validator.py "$skill"
done
```

### Quality Monitoring
```bash
# Score one skill at a time; `quality_scorer.py` has no batch option
python3 engineering/skill-tester/scripts/quality_scorer.py engineering/my-skill --json > quality_report.json
```

### Custom Scoring Thresholds
```bash
# Enforce minimum quality scores
python3 engineering/skill-tester/scripts/quality_scorer.py engineering/my-skill --minimum-score 80
# Exit code 0 = passed, 1 = failed, 2 = needs improvement
```

## Error Handling

All scripts provide comprehensive error handling:
- **File System Errors** - Missing files, permission issues, invalid paths
- **Content Errors** - Malformed YAML, invalid JSON, encoding issues  
- **Execution Errors** - Script timeouts, runtime failures, import errors
- **Validation Errors** - Standards violations, compliance failures

## Output Formats

### Human-Readable
```
=== SKILL VALIDATION REPORT ===
Skill: engineering/my-skill
Overall Score: 85.2/100 (B+)
Tier Recommendation: STANDARD

STRUCTURE VALIDATION:
  ✓ PASS: SKILL.md found
  ✓ PASS: README.md found
  ✓ PASS: scripts/ directory found

SUGGESTIONS:
  • Add references/ directory
  • Improve error handling in main.py
```

### JSON Format
```json
{
  "skill_path": "engineering/my-skill",
  "overall_score": 85.2,
  "letter_grade": "B+",
  "tier_recommendation": "STANDARD",
  "dimensions": {
    "Documentation": {"score": 88.5, "weight": 0.25},
    "Code Quality": {"score": 82.0, "weight": 0.25},
    "Completeness": {"score": 85.5, "weight": 0.25},
    "Usability": {"score": 84.8, "weight": 0.25}
  }
}
```

## Requirements

- **Python 3.7+** - No external dependencies required
- **File System Access** - Read access to skill directories  
- **Execution Permissions** - Ability to run Python scripts for testing

## Contributing

See [SKILL.md](SKILL.md) for comprehensive documentation and contribution guidelines.

The skill-tester itself serves as a reference implementation of POWERFUL-tier quality standards.