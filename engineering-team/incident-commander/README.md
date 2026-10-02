# Incident Commander Skill

A small set of Python scripts that format incident-response guidance from supplied incident data. They do not connect to monitoring, paging, ticketing, or status-page systems.

## Overview

This skill implements battle-tested practices from SRE and DevOps teams at scale, providing:

- **Rule-based severity suggestions** - Keyword, impact, and duration scoring against fixed rules; responders must confirm severity
- **Timeline formatting** - Organize supplied timestamped events and apply fixed phase/gap heuristics
- **PIR drafting** - Format supplied incident details using selected RCA prompts; generated text is not verified root-cause analysis
- **Communication Templates** - Pre-built stakeholder communication
- **Comprehensive Documentation** - Reference guides for incident response

## Quick Start

### Classify an Incident

```bash
# From JSON file
python scripts/incident_classifier.py --input incident.json --format text

# From stdin text
echo "Database is down affecting all users" | python scripts/incident_classifier.py --format text

# Interactive mode
python scripts/incident_classifier.py --interactive
```

### Reconstruct Timeline

```bash
# Analyze event timeline
python scripts/timeline_reconstructor.py --input events.json --format text

# With gap analysis
python scripts/timeline_reconstructor.py --input events.json --gap-analysis --format markdown
```

### Generate PIR Document

```bash
# Basic PIR
python scripts/pir_generator.py --incident incident.json --format markdown

# Comprehensive PIR with timeline
python scripts/pir_generator.py --incident incident.json --timeline timeline.json --rca-method fishbone
```

## Scripts

### incident_classifier.py

**Purpose:** Scores supplied descriptions and impact fields against fixed keyword/rule tables to suggest severity, teams, actions, and communication text. This is a triage aid, not an authoritative severity decision.

**Input:** JSON object with incident details or plain text description
**Output:** JSON + human-readable classification report

**Example Input:**
```json
{
  "description": "Database connection timeouts causing 500 errors",
  "service": "payment-api",
  "affected_users": "80%",
  "business_impact": "high"
}
```

**Key Features:**
- SEV1-4 severity suggestions from fixed keyword and impact scoring; validate against your incident policy
- Recommended response teams
- Initial action prioritization
- Communication templates
- Response timelines

### timeline_reconstructor.py

**Purpose:** Sorts supplied timestamped events, assigns phases using text patterns, and flags gaps using fixed thresholds. Verify timestamps, phase labels, and flagged gaps against source records.

**Input:** JSON array of timestamped events
**Output:** Formatted timeline with phase analysis and metrics

**Example Input:**
```json
[
  {
    "timestamp": "2024-01-01T12:00:00Z",
    "source": "monitoring",
    "message": "High error rate detected",
    "severity": "critical",
    "actor": "system"
  }
]
```

**Key Features:**
- Phase detection (detection → triage → mitigation → resolution)
- Duration analysis
- Gap identification
- Event-gap indicators; these do not measure communication effectiveness
- Response metrics

### pir_generator.py

**Purpose:** Drafts a Post-Incident Review from supplied incident and optional timeline JSON. RCA methods provide structured prompts and generated summaries; they do not establish or verify causation.

**Input:** Incident data JSON, optional timeline data
**Output:** Structured PIR document with RCA analysis

**Key Features:**
- Selectable analysis formats (5 Whys, Fishbone, Timeline, Bow Tie); human-led evidence review is required
- Action-item drafting from supplied data and templates; confirm owners, due dates, and success criteria
- Lessons learned categorization
- Follow-up planning
- Completeness assessment

## Sample Data

The `assets/` directory contains sample data files for testing:

- `sample_incident_classification.json` - Database connection pool exhaustion incident
- `sample_timeline_events.json` - Complete timeline with 21 events across phases
- `sample_incident_pir_data.json` - Comprehensive incident data for PIR generation
- `simple_incident.json` - Minimal incident for basic testing
- `simple_timeline_events.json` - Simple 4-event timeline

## Expected Outputs

The `expected_outputs/` directory contains reference outputs showing what each script produces:

- `incident_classification_text_output.txt` - Detailed classification report
- `timeline_reconstruction_text_output.txt` - Complete timeline analysis
- `pir_markdown_output.md` - Full PIR document
- `simple_incident_classification.txt` - Basic classification example

## Reference Documentation

### references/incident_severity_matrix.md
Complete severity classification system with:
- SEV1-4 definitions and criteria
- Response requirements and timelines
- Escalation paths
- Communication requirements
- Decision trees and examples

### references/rca_frameworks_guide.md  
Detailed guide for root cause analysis:
- 5 Whys methodology
- Fishbone (Ishikawa) diagram analysis
- Timeline analysis techniques
- Bow Tie analysis for high-risk incidents
- Framework selection guidelines

### references/communication_templates.md
Standardized communication templates:
- Severity-specific notification templates
- Stakeholder-specific messaging
- Escalation communications
- Resolution notifications
- Customer communication guidelines

## Usage Patterns

### End-to-End Incident Workflow

1. **Initial Classification**
```bash
echo "Payment API returning 500 errors for 70% of requests" | \
  python scripts/incident_classifier.py --format text
```

2. **Timeline Reconstruction** (after collecting events)
```bash
python scripts/timeline_reconstructor.py \
  --input events.json \
  --gap-analysis \
  --format markdown \
  --output timeline.md
```

3. **PIR Generation** (after incident resolution)
```bash
python scripts/pir_generator.py \
  --incident incident.json \
  --timeline timeline.json \
  --rca-method fishbone \
  --output pir.md
```

### Integration Examples

**CI/CD Pipeline Integration:**
```bash
# Classify deployment issues
cat deployment_error.log | python scripts/incident_classifier.py --format json
```

**Monitoring Integration:**
```bash
# Process alert events
curl -s "monitoring-api/events" | python scripts/timeline_reconstructor.py --format text
```

**Runbook Generation:**
Use classification output to automatically select appropriate runbooks and escalation procedures.

## Quality Standards

- **Zero External Dependencies** - All scripts use only Python standard library
- **Dual Output Format** - Both JSON (machine-readable) and text (human-readable)
- Input validation for supported JSON/text formats; inspect output and errors before relying on results
- Fixed example rules and templates; adapt and validate them against your incident policy
- **Comprehensive Testing** - Sample data and expected outputs included

## Technical Requirements

- Python 3.6+
- No external dependencies required
- Works with standard Unix tools (pipes, redirection)
- Cross-platform compatible

## Severity Classification Reference

| Severity | Description | Response Time | Update Frequency |
|----------|-------------|---------------|------------------|
| **SEV1** | Complete outage | 5 minutes | Every 15 minutes |
| **SEV2** | Major degradation | 15 minutes | Every 30 minutes |
| **SEV3** | Minor impact | 2 hours | At milestones |
| **SEV4** | Low impact | 1-2 days | Weekly |

## Getting Help

Each script includes comprehensive help:
```bash
python scripts/incident_classifier.py --help
python scripts/timeline_reconstructor.py --help  
python scripts/pir_generator.py --help
```

For methodology questions, refer to the reference documentation in the `references/` directory.

## Contributing

When adding new features:
1. Maintain zero external dependencies
2. Add comprehensive examples to `assets/`
3. Update expected outputs in `expected_outputs/`
4. Follow the established patterns for argument parsing and output formatting

## License

This skill is part of the claude-skills repository. See the main repository LICENSE for details.