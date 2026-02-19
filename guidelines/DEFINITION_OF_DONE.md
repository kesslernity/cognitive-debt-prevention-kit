# ✅ Definition of Done — AI-Assisted Development
# Version: 1.0 | Review cycle: Quarterly
# Source: https://www.talk-nerdy-to-me.com/blog/cognitive-debt-ai-coding-hidden-cost

---

## Purpose

This document defines what "done" means for any ticket or feature that involves AI-generated or AI-assisted code. It extends your existing DoD with cognitive debt-specific requirements.

Copy the checklist sections into your sprint board tool (Jira, Linear, Azure DevOps, etc.) as acceptance criteria templates.

---

## Standard DoD (Baseline — All Work)

These apply to all work regardless of AI involvement:

```
□ Code compiles and runs without errors
□ All existing tests pass
□ New functionality has unit and/or integration tests
□ Code has been peer reviewed and approved
□ No secrets or credentials committed
□ Branch merged to target branch
□ Ticket updated with resolution notes
□ Acceptance criteria from the ticket are met
□ Deployed and verified in staging
```

---

## Extended DoD — AI-Assisted Work

All items below apply when AI tools were used to generate or substantially assist any code in the ticket:

### Comprehension Requirements

```
□ Author can explain every function in their own words (tested at PR review time)
□ Author completed the AI explanation section in the PR template
□ No "TODO" or "FIXME" comments left from AI output without a tracked ticket
□ No dead code or unused imports left from AI generation
□ No new patterns introduced that conflict with MEMORY.md conventions
```

### Test Requirements

```
□ All AI-generated code paths have test coverage
□ Error paths and edge cases are explicitly tested (not just happy path)
□ Tests were written or reviewed by the author — not entirely AI-generated
□ No tests that only assert the happy path for functions with meaningful error behavior
```

### Documentation Requirements

```
□ MEMORY.md updated if any new pattern, convention, or architectural decision was introduced
□ Complex AI-generated functions have inline "why" comments (not just "what")
□ If a new abstraction was introduced, it is documented in MEMORY.md with rationale
```

### Review Requirements

```
□ Reviewer completed all five layers in CODE_REVIEW_GUARDRAILS.md
□ Reviewer can independently explain what the AI-generated code does
□ No silent failure patterns approved (swallowed exceptions, default returns masking failures)
□ PR labeled with "ai-assisted" for metrics tracking
□ If code is in or adjacent to an AI-Free Zone: lead sign-off obtained
```

### Security Requirements (Mandatory for Auth, Payments, Data Paths)

```
□ All inputs validated before use
□ No parameterized query violations
□ No secrets in logs, error messages, or responses
□ Security review obtained if touching auth, payments, or data deletion
```

---

## Tiered DoD by Risk Level

Not all AI-assisted work carries the same risk. Apply the appropriate tier based on where the code lives:

### Tier 1 — Standard (Boilerplate, Internal Tools, Non-Critical Features)
Apply the Standard DoD + Comprehension and Test requirements above.

### Tier 2 — Elevated (User-Facing Features, External APIs, Database Interactions)
Apply everything in Tier 1, plus:
```
□ Integration tests cover the new code path
□ Error handling reviewed specifically for silent failure patterns
□ Rollback plan documented in the PR
□ Monitoring/alerting exists for the new code path
```

### Tier 3 — High-Risk (Auth, Payments, Data Deletion, Migrations)
Apply everything in Tier 1 and 2, plus:
```
□ Code was authored or rewritten by a human (not purely AI-generated)
□ Tech lead or senior engineer has reviewed specifically for correctness
□ Dedicated QA testing in staging environment
□ Rollback procedure tested and documented
□ Post-deploy monitoring plan in place for first 48 hours
```

---

## Sprint-Level DoD

Before a sprint is considered complete:

```
□ All AI-Free Zone violations identified this sprint were resolved or escalated
□ MEMORY.md reflects any new patterns introduced during the sprint
□ Cognitive Debt Pulse metrics reviewed in sprint retrospective:
    - AI-generated code % of sprint output
    - PRs where comprehension could not be confirmed
    - Any "unknown why" in incident or debugging notes this sprint
□ Comprehension review session held (or scheduled if backlogged)
□ Any cognitive debt concerns raised this sprint have documented outcomes
```

---

## Acceptance Criteria Template (Copy Into Your Ticket Tool)

For use when creating tickets for AI-heavy work:

```
Acceptance Criteria — Cognitive Debt Standards:

- [ ] Author can explain all AI-generated code without re-reading it
- [ ] AI explanation completed in PR template
- [ ] Test coverage includes error paths and identified edge cases
- [ ] No silent failure patterns introduced
- [ ] MEMORY.md updated if new patterns were introduced
- [ ] Reviewer confirmed comprehension (Layer 1 of code review guardrails)
- [ ] AI-Free Zone check: code does not touch [list relevant zones]
```

---

## Why This Matters

The Definition of Done is your last line of defense before cognitive debt enters production. It works only if everyone treats it as a genuine bar, not a checklist to rush through.

> "Done means understood, tested, documented, and owned — not just shipped."

---
*Part of the [Cognitive Debt Prevention Kit](https://github.com/kesslernity/cognitive-debt-prevention-kit) by [Kesslernity](https://kesslernity.com)*
