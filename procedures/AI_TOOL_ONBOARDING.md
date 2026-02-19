# 🚀 AI Tool Onboarding Procedure
# For: New team members + any engineer adopting a new AI coding tool
# Version: 1.0 | Review cycle: Quarterly
# Source: https://www.talk-nerdy-to-me.com/blog/cognitive-debt-ai-coding-hidden-cost

---

## Purpose

Before using AI coding tools on this codebase, every engineer must complete this onboarding. It ensures AI tools are used actively — not passively — and that the team's cognitive debt prevention practices are understood before the first PR.

Estimated time: **90 minutes** (reading + exercises)

---

## Step 1: Read the Foundation Documents (30 min)

Complete these before touching any AI tool on this codebase:

| Document | Location | Purpose |
|----------|----------|---------|
| Cognitive Debt — the concept | [Article link or internal doc] | Why these practices exist |
| `templates/MEMORY.md` | Repo root | Architecture, conventions, AI-Free Zones |
| `AI_USAGE_GUIDELINES.md` | `/guidelines/` | What's permitted, what isn't |
| `templates/COGNITIVE_DEBT_CHECKLIST.md` | Repo root | Your daily workflow checkpoint |
| `CODE_REVIEW_GUARDRAILS.md` | `/guidelines/` | What reviewers expect from you |
| `DEFINITION_OF_DONE.md` | `/guidelines/` | What "done" means for AI-assisted work |

**After reading, you should be able to answer:**
- What is cognitive debt and how does it differ from technical debt?
- What are the five patterns to prevent it?
- What are the AI-Free Zones for this codebase?
- What are the three questions in the comprehension checkpoint?
- What must a PR contain if AI was used?

If you can't answer these after reading, ask your lead before proceeding.

---

## Step 2: Comprehension Exercise (20 min)

Before writing any AI-assisted code, practice the comprehension pattern on existing code.

**Exercise:**
1. Pick any recently merged PR in this repo (last 2 weeks) that contains non-trivial logic
2. Read the code without the PR description
3. Write a plain-English explanation of what the code does and why the approach was chosen
4. Read the PR description — how close were you?
5. Identify one thing you'd have asked in review if you were the reviewer

**Goal:** Calibrate your comprehension standard against the team's existing codebase before introducing AI-generated code.

---

## Step 3: AI Tool Configuration Checklist (15 min)

Before your first AI-assisted session:

### Data Privacy
```
□ Confirmed your AI tool is on the approved tools list (see AI_USAGE_GUIDELINES.md)
□ Checked company data handling policy for AI tools
□ Configured tool to [send / not send] code to external servers per policy
□ Confirmed no sensitive environment variables or secrets are in scope
```

### Context Setup
```
□ MEMORY.md is open and accessible (pin it in your editor)
□ AI tool's context/system prompt updated with relevant MEMORY.md content (if supported)
   → Copy the Architecture Decisions, Security Constraints, and Naming Conventions
   → This keeps the AI generating code consistent with your codebase
□ Confirmed which paths are AI-Free Zones — these are off-limits for AI output
```

### Workspace Habits
```
□ Terminal / IDE arranged so you can see code and tests simultaneously
□ Test runner available to verify AI output immediately after generation
□ Git configured with your name — all AI-disclosed commits attributed to you (you own what you merge)
```

---

## Step 4: First PR Walkthrough (25 min)

Your first AI-assisted PR on this codebase must be reviewed by your tech lead or a senior engineer — not a standard peer review.

**Before submitting:**
1. Complete the Cognitive Debt Checklist for every AI-generated block
2. Fill in the PR template AI explanation section carefully — your lead will be checking it
3. Verify you've tagged the PR with `ai-assisted`
4. Do a self-review: can you explain every function in your own words?

**During review:**
Your reviewer will walk through CODE_REVIEW_GUARDRAILS.md with you, not just approve or reject. This is a calibration conversation, not a gate.

**After review:**
Note any feedback on comprehension standards for future reference.

---

## Step 5: Sign-Off

After completing Steps 1–4, confirm:

```
I have read:
□ MEMORY.md (current version)
□ AI_USAGE_GUIDELINES.md
□ templates/COGNITIVE_DEBT_CHECKLIST.md
□ CODE_REVIEW_GUARDRAILS.md
□ DEFINITION_OF_DONE.md

I understand:
□ The active vs. passive AI use pattern
□ The AI-Free Zones for this codebase
□ The PR disclosure requirements
□ The three comprehension checkpoint questions
□ When and how to escalate a cognitive debt concern

My first AI-assisted PR has been reviewed and calibrated with: [tech lead name]

Name: _________________ Date: _________________
```

Share this with your tech lead. File it wherever your team keeps onboarding records.

---

## Ongoing: Monthly Self-Check

After onboarding, use this 5-minute monthly self-check to catch drift:

```
Last 30 days:
□ Did I always complete the AI explanation section in PRs?
□ Did I always run the comprehension checkpoint before accepting AI code?
□ Did I update MEMORY.md when I introduced a new pattern?
□ Did I encounter any code I couldn't explain — and did I raise it?
□ Did I apply the active pattern (I defined architecture; AI filled implementation)?

If any box is unchecked: identify why and adjust your workflow before next month.
```

---

## Reference: Active vs. Passive Pattern Summary

```
YOU DEFINE:                   AI GENERATES:
─────────────────────────     ─────────────────────────
Function signatures           Implementation body
Type definitions              Boilerplate and repetition
Interfaces & contracts        Test bodies (for your cases)
Algorithm approach            Documentation first draft
Test cases & edge cases       Refactored code (for your patterns)
Architecture decisions        Code in non-AI-Free areas

YOU ALWAYS:
─────────────────────────────────────────────────────────
Trace data flow before accepting
Run tests before committing
Explain code in your own words before submitting for review
Update MEMORY.md when patterns change
Own everything you merge — no exceptions
```

---
*Part of the [Cognitive Debt Prevention Kit](https://github.com/kesslernity/cognitive-debt-prevention-kit) by [Kesslernity](https://kesslernity.com)*
