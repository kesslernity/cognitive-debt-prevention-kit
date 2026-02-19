# 📘 Cognitive Debt — Team Playbook for Engineering Leads
# Source: https://www.talk-nerdy-to-me.com/blog/cognitive-debt-ai-coding-hidden-cost

> "Cognitive debt compounds silently. By the time you notice the interest payments, the principal is already unmanageable."
> — Martin Fowler (via Talk Nerdy to Me)

---

## What This Playbook Is

A practical system for managing cognitive debt at the team level.  
Individual developer habits help. But without team-level enforcement, the incentives always favor speed over comprehension.  
This playbook gives you the ceremonies, metrics, and gates to make cognitive debt management a team habit — not a personal one.

---

## 📐 The Four Team Practices

### 1. Establish Your AI-Free Zones (Day 1)

Some code paths are too consequential for cognitive debt.  
Define these as a team. Enforce them in your PR process.

**Template — AI-Free Zone Declaration:**

```markdown
## AI-Free Zones — [Team Name]

The following paths require human-written or human-rewritten code.
AI may be used to draft. A human engineer must own, understand, and rewrite.

| Path | Risk Reason | Owner |
|------|-------------|-------|
| src/auth/ | Authentication & authorization | [name] |
| src/payments/ | Payment processing | [name] |
| src/data/deletion* | Data deletion (compliance risk) | [name] |
| src/migrations/ | Schema migrations (irreversible) | [name] |
| [add yours] | | |

Review these quarterly. Add paths after any incident linked to AI-generated code.
```

---

### 2. Add Comprehension Reviews to Your Sprint

This is not a code review. It's a reading exercise.

**Format:**
- **Frequency:** Once per sprint (or once per two weeks)
- **Duration:** 60–90 minutes
- **Who:** Rotating pairs (not the original author)
- **Focus:** AI-heavy PRs merged in the last sprint, especially on critical paths
- **Output:** Updated MEMORY.md entries, inline comments, or flagged rewrites

**Facilitation checklist:**
- [ ] Pull list of AI-assisted PRs from last sprint (use GitClear / CodeRabbit labels, or PR tags)
- [ ] Assign pairs — never the original author reviewing their own work
- [ ] Each pair reads the code, adds "why" comments, updates MEMORY.md
- [ ] Any code nobody can explain gets flagged for rewrite in next sprint

---

### 3. Track the Right Metrics

Technical debt has JIRA tickets. Cognitive debt has proxy metrics.  
Track these each sprint. Trend matters more than any single number.

| Metric | Source | Red Flag Threshold |
|--------|--------|--------------------|
| MTTR (AI-heavy files) | Incident log | >2x MTTR of non-AI files |
| Code churn rate | GitClear / git log | Rising trend over 3+ sprints |
| "Unknown why" in postmortems | Incident postmortem docs | Any occurrence |
| AI-generated code % of codebase | CodeRabbit / GitClear | >40% without comprehension reviews |
| PR review time on AI code | GitHub insights | Rising without size increase |
| Test coverage on AI paths | Coverage report | <90% on any production path |

**Sprint review addition:**
> Add a 5-minute "Cognitive Debt Pulse" to every sprint review:
> - What's our churn rate this sprint?
> - Any incidents where the root cause was code nobody understood?
> - Did comprehension reviews surface anything that needs rewrite?

---

### 4. Enforce the PR Gate

The PR template (`.github/PULL_REQUEST_TEMPLATE.md`) is your main enforcement mechanism.  
But templates only work if reviewers hold the line.

**Reviewer brief — share this with your team:**

```markdown
## Reviewer Standard for AI-Assisted Code

When reviewing a PR that contains AI-generated code:

1. Read the AI Explanation section in the PR description FIRST.
   If it's missing or vague, request it before reviewing the code.

2. Ask yourself: does the explanation match what the code actually does?
   If not, that's a signal the author doesn't fully understand it yet.

3. Check for silent failure patterns:
   - Bare catch blocks that swallow errors
   - Default return values hiding failures
   - TODO/FIXME comments left from AI output

4. If you can't explain what a function does after reading it,
   ask the author — don't approve. Confusion in review = incident in production.

5. If the PR is >200 lines of meaningful change, ask for it to be split.
   You cannot review what you cannot hold in your head.
```

---

## 📊 Quarterly Cognitive Debt Audit

Run this every quarter. Takes ~2 hours for a team of 5.

**Step 1: Identify high-risk files**
```bash
# Files with highest churn in the last 90 days
git log --since="90 days ago" --diff-filter=M --name-only --format="" | sort | uniq -c | sort -rn | head -20
```

**Step 2: Cross-reference with AI origin**
- Use GitClear's AI-detection report, or
- Review commit messages / PR labels for AI-assisted flags
- Flag files that are both high-churn AND AI-generated

**Step 3: Comprehension test**
For each flagged file, answer as a team:
- Can at least two engineers explain what this code does and why?
- Is this code covered by tests that would catch a regression?
- Is this code in a critical path (auth, payments, data deletion)?

**Step 4: Produce the Audit Output**

```markdown
## Cognitive Debt Audit — [Quarter] [Year]

### High-Risk Files Identified
| File | Churn (90d) | AI-Generated? | Understood by 2+ engineers? | Action |
|------|-------------|---------------|------------------------------|--------|
| | | | | |

### Incidents Linked to Cognitive Debt
| Incident | Date | AI Code Involved? | MTTR | Notes |
|----------|------|-------------------|------|-------|
| | | | | |

### Actions for Next Quarter
- [ ] Rewrite: [files flagged as high-risk + not understood]
- [ ] Document: [files understood but underdocumented]
- [ ] Add to AI-Free Zones: [files that caused incidents]
- [ ] Comprehension reviews scheduled: [dates]
```

---

## 🚨 Incident Postmortem Addition

Add this section to your postmortem template for every production incident:

```markdown
## Cognitive Debt Assessment

- Was the root-cause code AI-generated or AI-assisted? [ ] Yes [ ] No [ ] Unknown
- Could the on-call engineer explain the code's behavior before the incident? [ ] Yes [ ] No
- Was the bug of a type that a developer deeply familiar with the code would have caught? [ ] Yes [ ] No
- Was this code in a declared AI-Free Zone? [ ] Yes [ ] No

**If any answer suggests cognitive debt contributed:**
- Add the affected file to the quarterly audit watchlist
- Schedule a comprehension review for the affected module
- Consider adding the path to AI-Free Zones
```

---

## 🎓 Onboarding Addition

When onboarding new engineers into AI-assisted codebases:

```markdown
## Day 1 Briefing — Cognitive Debt & AI Code

We use AI coding tools. Here's how we manage the risks:

1. Read MEMORY.md before writing any code. It's the canonical "why" for this codebase.

2. The PR template has an AI explanation section. If you used AI, you must complete it.
   If you can't explain the code in your own words, ask for help before submitting.

3. Check the AI-Free Zones list before starting any task in auth, payments, or data deletion.
   Those areas require human-written code.

4. If you inherit code you can't explain, flag it in standup. We'd rather know now.

5. Comprehension is a team metric, not a personal one. Nobody is expected to understand everything alone.
```

---

## 📎 Quick Reference

| Tool | Use For |
|------|---------|
| [GitClear](https://www.gitclear.com) | Code churn analysis, AI-flagged code detection |
| [CodeRabbit](https://coderabbit.ai) | AI quality review in PRs, logic error detection |
| MEMORY.md | Shared context for AI agents and humans alike |
| `.github/PULL_REQUEST_TEMPLATE.md` | PR comprehension gate |
| `templates/COGNITIVE_DEBT_CHECKLIST.md` | Individual developer pre-accept checkpoint |
| Incident postmortem template | Cognitive debt attribution in incidents |

---

*Cognitive debt is a team problem. Manage it like one.*
*Individual discipline helps. System-level enforcement scales.*

---
*Part of the [Cognitive Debt Prevention Kit](https://github.com/kesslernity/cognitive-debt-prevention-kit) by [Kesslernity](https://kesslernity.com)*
