# claude-skills

> **235 production-ready Claude Code skills for 11 AI coding agents** — engineering, DevOps, marketing, compliance, C-level advisory, and more

<p align="center">
  <a href="https://github.com/hmzainjamil/claude-skills/stargazers"><img src="https://img.shields.io/github/stars/hmzainjamil/claude-skills?style=for-the-badge&labelColor=555&color=yellow" alt="Stars"/></a>
  <a href="https://github.com/hmzainjamil/claude-skills/network/members"><img src="https://img.shields.io/github/forks/hmzainjamil/claude-skills?style=for-the-badge&labelColor=555&color=blue" alt="Forks"/></a>
  <a href="https://github.com/hmzainjamil/claude-skills/issues"><img src="https://img.shields.io/github/issues/hmzainjamil/claude-skills?style=for-the-badge&labelColor=555&color=red" alt="Issues"/></a>
  <a href="https://github.com/hmzainjamil/claude-skills/pulls"><img src="https://img.shields.io/github/issues-pr/hmzainjamil/claude-skills?style=for-the-badge&labelColor=555&color=purple" alt="PRs"/></a>
  <a href="https://github.com/hmzainjamil/claude-skills/commits/main"><img src="https://img.shields.io/github/last-commit/hmzainjamil/claude-skills?style=for-the-badge&labelColor=555&color=green" alt="Last Commit"/></a>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Skills-235-brightgreen?style=flat&labelColor=555"/>
  <img src="https://img.shields.io/badge/Python_tools-305-blue?style=flat&labelColor=555"/>
  <img src="https://img.shields.io/badge/Agents_supported-11-orange?style=flat&labelColor=555"/>
  <img src="https://img.shields.io/badge/Stars-5200%2B-yellow?style=flat&labelColor=555"/>
  <img src="https://img.shields.io/badge/License-MIT-lightgrey?style=flat&labelColor=555"/>
</p>

---

## Why This Exists

Claude Code doesn't know your specific domain out of the box. It doesn't know your company's coding standards, your client's industry terminology, your compliance requirements, or your team's preferred patterns. Skills fix this: each SKILL.md is a loadable expertise package that gives Claude instant domain knowledge — backend architecture, marketing strategy, legal review, security auditing, DevOps automation.

**5,200+ GitHub stars.** The most comprehensive open-source Claude Code skills library. Also works with Codex, Gemini CLI, Cursor, Aider, Windsurf, and 6 more agents.

---

## At a Glance

| Category | Skills | Description |
|---|---|---|
| Engineering | 80+ | Backend, frontend, DevOps, testing, architecture |
| Marketing | 30+ | SEO, ads, email, content, social, analytics |
| Security | 20+ | Pen testing, SAST, compliance, audits |
| Data | 15+ | SQL, ML pipelines, visualization, ETL |
| C-Level Advisory | 8+ | CEO, CTO, CMO, CFO, CPO advisors |
| Legal | 10+ | NDA review, contracts, compliance, GDPR |
| DevOps | 25+ | CI/CD, Kubernetes, Terraform, monitoring |
| Product | 12+ | PRD writing, roadmaps, user research |
| Personas | 3 | Named character agents |
| CLI tools | 305 | stdlib-only Python tools |

---

## 🧠 CONCEPTS

| Concept | Description |
|---|---|
| **SKILL.md** | Instruction file: role, context, steps, examples, anti-patterns |
| **Skill** | SKILL.md + optional Python tools = loadable expertise package |
| **Agent skill** | Skill designed for autonomous execution without human approval |
| **Persona** | Named character with specific communication style |
| **CLI tool** | stdlib-only Python script — zero pip installs required |
| **Skill router** | Hook that auto-detects prompt keywords and loads matching skills |
| **Convert script** | `scripts/convert.sh` — converts skills to 8 other agent formats |
| **SkillCheck** | Automated validation that skills meet quality standards |
| **Trigger keywords** | Words in SKILL.md that activate skill-router auto-loading |
| **Scope** | Which agent(s) a skill targets: Claude Code, Codex, both, all |

### 🔥 Hot

- **305 zero-dependency Python tools** — every CLI tool runs on stdlib only. No pip installs, works on any system with Python
- **11-agent compatibility** — one skill format, converts to Claude Code, Codex, Gemini CLI, Cursor, Aider, Windsurf, Kilo, OpenCode, Augment, Antigravity via `convert.sh`
- **C-level advisors** — install CEO/CTO/CMO advisor skills to get strategic-level input on any decision
- Source → [HMZ](https://github.com/hmzainjamil)

---

## ⚙️ HOW IT WORKS

```
1. Install skill
   cp -r skills/backend-architect ~/.claude/skills/

2. Load in session
   /backend-architect        # Manual activation
   # OR: skill-router auto-loads on keyword match

3. Claude now has backend architecture expertise
   "Design microservices for this e-commerce platform"
   → Expert response with specific patterns, tradeoffs, diagrams
```

---

## 🚀 INSTALL

```bash
# Clone
git clone https://github.com/hmzainjamil/claude-skills

# Install all skills
cp -r claude-skills/skills/* ~/.claude/skills/

# Install specific skill
cp -r claude-skills/skills/backend-architect ~/.claude/skills/

# Install for other agents
bash claude-skills/scripts/convert.sh --target codex
bash claude-skills/scripts/convert.sh --target gemini-cli

# Verify
ls ~/.claude/skills/
```

---

## 📟 USAGE

```bash
# Manual activation
/backend-architect
/senior-devops
/cmo-advisor
/security-auditor

# List available skills
ls ~/.claude/skills/

# Search skills by keyword
grep -r "kubernetes" ~/.claude/skills/*/SKILL.md

# Convert to other agent
bash scripts/convert.sh --skill backend-architect --target cursor

# Run CLI tool
python ~/.claude/skills/sql-pro/tools/analyze_query.py "SELECT * FROM users"
```

---

## ⚙️ CONFIGURATION

| Setting | Default | Description |
|---|---|---|
| `SKILL_DIR` | `~/.claude/skills/` | Skills installation directory |
| `SKILL_ROUTER` | `true` | Auto-load skills via keyword matching |
| `SKILL_MAX_LOADED` | `5` | Max skills loaded simultaneously |
| `SKILL_COMPACT` | `false` | Use compact skill variants |
| `DEFAULT_SCOPE` | `claude-code` | Target agent for skill loading |
| `TRIGGER_THRESHOLD` | `0.7` | Confidence threshold for auto-activation |
| `SKILL_CACHE` | `true` | Cache loaded skills for session |
| `LOG_ACTIVATIONS` | `false` | Log which skills activate per prompt |
| `CONVERT_FORMAT` | `claude-code` | Default format for convert.sh |
| `VALIDATE` | `true` | Run SkillCheck validation on install |

---

## 💡 TIPS AND TRICKS

### Performance
1. **Batch skill installs** — install all skills at once, not one-by-one. Copy entire `skills/` dir. Source → [HMZ](https://github.com/hmzainjamil)
2. **Skill router** — add `skill-router` to `UserPromptSubmit` hook to auto-load skills without manual activation. Source → [HMZ](https://github.com/hmzainjamil)
3. **Compact skills** — each SKILL.md should be <2KB. Large skills bloat context on every request. Source → [HMZ](https://github.com/hmzainjamil)

### Integration
4. **Project-specific CLAUDE.md** — load domain skills only in relevant projects. Don't load SEO skills in backend repos. Source → [HMZ](https://github.com/hmzainjamil)
5. **Skill versioning** — pin skill versions in projects. Skills evolve — unexpected behavior changes break workflows. Source → [HMZ](https://github.com/hmzainjamil)
6. **SKILL.md structure** — Role → Context → Steps → Examples → Anti-patterns. This order maximizes Claude compliance. Source → [HMZ](https://github.com/hmzainjamil)

### Advanced
7. **Python tools** — SKILL.md + stdlib-only Python scripts. Zero pip installs — works everywhere Python runs. Source → [HMZ](https://github.com/hmzainjamil)
8. **Multi-agent skills** — skills designed for parallel agents should be stateless — no file writes, pure output. Source → [HMZ](https://github.com/hmzainjamil)
9. **Cross-platform** — test skills on Claude Code AND Codex before publishing. Behavior differs subtly. Source → [HMZ](https://github.com/hmzainjamil)

### Debugging
10. **Skill not loading** — check SKILL.md is valid UTF-8, no null bytes, under 4KB. Source → [HMZ](https://github.com/hmzainjamil)
11. **Skill conflicts** — two skills with overlapping instructions → unpredictable behavior. Source → [HMZ](https://github.com/hmzainjamil)
12. **Log skill activations** — add logging to skill-router hook to track which skills load per prompt. Source → [HMZ](https://github.com/hmzainjamil)


---

## 🔧 TROUBLESHOOTING

| Issue | Cause | Fix |
|---|---|---|
| Skill not activating | Keywords not in prompt | Check trigger keywords in SKILL.md |
| Context overflow | Too many skills loaded | Unload unused skills, use compact variants |
| Skill ignored | CLAUDE.md conflicts | Check for conflicting instructions |
| Python tools failing | Wrong Python version | Tools require Python 3.8+ |
| Install path wrong | Skills not in `~/.claude/skills/` | Move to correct directory |
| Skill works in chat not code | Tool mode differences | Test with `claude --tool` flag |

---

## 📊 ARCHITECTURE

```
~/.claude/skills/
├── skill-name/
│   ├── SKILL.md          # Instructions, steps, anti-patterns
│   └── tools/
│       └── tool.py       # stdlib-only Python tool
```

**Loading order:** CLAUDE.md → skill-router hook detects keywords → loads matching SKILL.md → Claude reads instructions → executes with domain expertise

---

## 🗺️ ROADMAP

- [ ] Skill marketplace — search and install skills from CLI
- [ ] Skill versioning — semantic versioning for skills
- [ ] Automated skill testing — eval harness per skill
- [ ] Skill analytics — track which skills are most used
- [ ] Cross-agent skill format — universal format for all coding agents

---

## ☠️ STARTUPS / BUSINESSES

Skills are the fastest way to give Claude domain expertise it doesn't have by default. Instead of writing domain context in every prompt, install it once and Claude knows it forever.

**Agency use:** install marketing, SEO, and ads skills → Claude handles all client deliverables without domain-specific prompting. Every team member gets expert-level output automatically.

---

## Star History

[![Star History Chart](https://api.star-history.com/svg?repos=hmzainjamil/claude-skills&type=Date)](https://star-history.com/#hmzainjamil/claude-skills&Date)

---

<p align="center">
  Built by <a href="https://github.com/hmzainjamil">HMZ</a> · <a href="https://github.com/hmzainjamil/claude-skills/issues">Issues</a> · <a href="https://github.com/hmzainjamil/claude-skills/pulls">PRs</a>
</p>
