<div align="center">

# Cognitive Debt Prevention Kit

**By [Kesslernity](https://kesslernity.com) — Standardizing the 2026 AI Workforce**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)
[![Maintained by Kesslernity](https://img.shields.io/badge/maintained%20by-Kesslernity-blueviolet)](https://kesslernity.com)

*You ship faster with AI. You understand less. That gap has a name — and this kit fixes it.*

[**Read the full article**](https://www.talk-nerdy-to-me.com/blog/cognitive-debt-ai-coding-hidden-cost) · [**Explore Kesslernity**](https://kesslernity.com)

</div>

---

## What Is Cognitive Debt?

Every time you accept AI-generated code without fully understanding it, you take on **cognitive debt** — the growing gap between what your codebase does and what your team actually comprehends about it.

Unlike technical debt (code you know is bad), cognitive debt is **code you don't even know is bad** — because you never fully understood it in the first place.

The numbers are real:
- **19% slower** — METR study, experienced devs using AI tools vs. not (2025)
- **+23.5% more incidents per PR** — Cortex 2026 Engineering Benchmark
- **Trust in AI output dropped to 33%** — Stack Overflow 2025, even as usage hit 76%
- **Code churn nearly doubled** (3.1% → 5.7%) — GitClear analysis

This kit gives your team everything needed to use AI tools actively — without losing comprehension of your own systems.

---

## What's in the Kit

```
cognitive-debt-prevention-kit/
│
├── templates/                         Core files for every repo
│   ├── MEMORY.md                      Living AI context & architecture decisions
│   ├── COGNITIVE_DEBT_CHECKLIST.md    Developer's pre-accept checkpoint card
│   └── TEAM_PLAYBOOK.md              Sprint ceremonies & quarterly audit system
│
├── .github/
│   └── PULL_REQUEST_TEMPLATE.md       PR comprehension gate with AI declaration
│
├── guidelines/                        The standards everyone must know
│   ├── AI_USAGE_GUIDELINES.md         Permitted/prohibited use, roles, disclosure
│   ├── CODE_REVIEW_GUARDRAILS.md      5-layer review framework for AI code
│   └── DEFINITION_OF_DONE.md         Tiered DoD for AI-assisted tickets
│
└── procedures/                        What to do when things happen
    ├── AI_TOOL_ONBOARDING.md          90-min onboarding before first AI PR
    ├── INCIDENT_RESPONSE_PROCEDURE.md Phases 1-5 for AI-related incidents
    └── ESCALATION_PROCEDURE.md        When/how to raise cognitive debt concerns
```

---

## The Core Concept: Active vs. Passive

| Pattern | Workflow | Outcome |
|---------|----------|---------|
| **Active ✅** | Prompt → Read → Understand → Modify → Ship | Comprehension maintained |
| **Passive ❌** | Prompt → Accept → Ship → Forget | Cognitive debt accumulates |

**The difference between these two patterns determines whether AI coding tools are a productivity multiplier or a cognitive debt factory.**

---

## Quick Start

### For a single developer (5 min)

```bash
# Clone or fork this repo, then copy what you need:
cp templates/MEMORY.md /your-project/MEMORY.md
cp templates/COGNITIVE_DEBT_CHECKLIST.md /your-project/templates/COGNITIVE_DEBT_CHECKLIST.md
cp .github/PULL_REQUEST_TEMPLATE.md /your-project/.github/PULL_REQUEST_TEMPLATE.md
```

Open `templates/MEMORY.md` and fill in your architecture decisions. The act of writing it is itself the first cognitive debt prevention exercise.

### For an engineering team (30 min)

1. **Fork this repo** and customize for your codebase
2. **Fill in `templates/MEMORY.md` as a team** — architecture decisions, security constraints, naming conventions, AI-Free Zones
3. **Deploy the PR template** — GitHub picks up `.github/PULL_REQUEST_TEMPLATE.md` automatically
4. **Share the guidelines** — `AI_USAGE_GUIDELINES.md` is your team policy; `CODE_REVIEW_GUARDRAILS.md` is your reviewer standard
5. **Onboard everyone** via `procedures/AI_TOOL_ONBOARDING.md` before their first AI-assisted PR
6. **Schedule a comprehension review** for next sprint — block 90 minutes, assign pairs, focus on your AI-heaviest recent PRs

### For an engineering lead (45 min)

Complete the team steps above, then:
- Define your **AI-Free Zones** in `templates/MEMORY.md` (auth, payments, migrations, data deletion)
- Add the `ai-assisted` label to your PR tracker
- Set a calendar reminder for the **quarterly cognitive debt audit** (see `templates/TEAM_PLAYBOOK.md`)
- Brief your team with the 15-min standup format in `templates/TEAM_PLAYBOOK.md`

---

## The Five Prevention Patterns

This kit operationalizes the five patterns from the [original research](https://www.talk-nerdy-to-me.com/blog/cognitive-debt-ai-coding-hidden-cost):

| # | Pattern | Kit File |
|---|---------|----------|
| 1 | Maintain a `templates/MEMORY.md` — living architecture context for you and your AI | `templates/MEMORY.md` |
| 2 | Explain Before Merge — comprehension gate in every PR | `.github/PULL_REQUEST_TEMPLATE.md` |
| 3 | Comprehension Checkpoints — three questions before you accept AI output | `templates/COGNITIVE_DEBT_CHECKLIST.md` |
| 4 | Pair with Agents, Don't Delegate — you steer, AI fills | `guidelines/AI_USAGE_GUIDELINES.md` |
| 5 | Shrink the Blast Radius — <200 lines, 1 concern, 100% coverage on AI paths | `guidelines/DEFINITION_OF_DONE.md` |

---

## Document Map

How the ten files connect across your team's workflow:

```
NEW ENGINEER JOINS
    └──► AI_TOOL_ONBOARDING ──► MEMORY.md + AI_USAGE_GUIDELINES

DAILY DEVELOPMENT  
    ├──► COGNITIVE_DEBT_CHECKLIST   (before accepting AI output)
    ├──► MEMORY.md                  (open in editor at all times)
    └──► PULL_REQUEST_TEMPLATE      (before every PR)

CODE REVIEW
    └──► CODE_REVIEW_GUARDRAILS ──► DEFINITION_OF_DONE

SOMETHING GOES WRONG
    ├──► ESCALATION_PROCEDURE       (concern identified early)
    └──► INCIDENT_RESPONSE          (production incident)

SPRINT & QUARTERLY RITUALS
    └──► TEAM_PLAYBOOK ──► MEMORY.md (audit output)
```

---

## AI-Free Zones

Some code paths are too consequential for cognitive debt. This kit includes a framework for declaring them and enforcing them in your review process. The default list to start from:

- Authentication & authorization
- Payment processing
- Data deletion (compliance risk)
- Database migrations (irreversible)

> AI may draft. A human must own, understand, and rewrite.

---

## Contributing

Found a gap? Improved a template for your team? PRs are welcome.

See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines. This kit improves when teams share what worked and what didn't.

---

## About Kesslernity

[Kesslernity](https://kesslernity.com) builds AI infrastructure for enterprises — prompt libraries, training programs, and adoption systems that prevent teams from moving fast and understanding nothing.

This kit is open-source and free to use under the MIT license.

---

## License

MIT — free to use, fork, adapt, and distribute. Attribution appreciated but not required.

---

<div align="center">

*Never ship code you can't explain.*

**[kesslernity.com](https://kesslernity.com)**

</div>
