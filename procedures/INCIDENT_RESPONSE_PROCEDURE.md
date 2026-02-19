# Incident Response Procedure — AI-Generated Code
# Version: 1.0 | Review cycle: After every relevant incident

---

## Purpose

When a production incident involves AI-generated code, the standard incident response process must include an additional layer: **cognitive debt assessment**. This procedure defines the steps, roles, and outputs required.

This document supplements — it does not replace — your existing incident response runbook.

---

## Trigger Criteria

Use this procedure when **any** of the following is true during an active incident or post-incident review:

- The failing code was identified as AI-generated or AI-assisted during authorship
- No team member can immediately explain why the code behaves the way it does
- The bug is in a function nobody "owns" mentally
- The PR author says "I'm not sure what this part does" during triage
- The incident involves a silent failure (no alarms fired, data silently corrupted)

---

## Phase 1: During Active Incident (First 30 Minutes)

### Immediate Actions

**Step 1 — Identify the blast radius**
```
□ What systems are affected?
□ Is data corrupted / lost / exposed? (If yes: escalate immediately to data incident track)
□ Is revenue / payments impacted? (If yes: escalate to financial incident track)
□ What is the current failure mode — total outage, degraded, or silent?
```

**Step 2 — Assess AI code involvement**
```
□ Is the failing code AI-generated or AI-assisted?
   → Check git blame → Check PR labels (ai-assisted) → Ask the author

□ If YES: Does anyone on the current response team understand what the code does?
   → If NO: Page the original author immediately, even outside business hours.
   → Do NOT attempt to patch code nobody understands under pressure.
```

**Step 3 — Stabilize first, understand second**

Priority order:
1. **Revert** the PR that introduced the failing code (if identifiable and low-risk to revert)
2. **Feature flag off** the failing functionality (if flag exists)
3. **Route around** the failure at the infrastructure level if revert is risky
4. **Patch** only once someone who understands the code is on the call

> **Critical:** Do not use AI to generate a hotfix for AI-generated code you don't understand. This is how cognitive debt compounds into a cascade.

---

## Phase 2: Investigation (During Stabilization)

While the system is being stabilized, a parallel track investigates root cause.

### Cognitive Debt Assessment

Answer these questions during investigation and record answers in the incident doc:

| Question | Answer |
|----------|--------|
| Was the failing code AI-generated? | Yes / No / Unknown |
| Did the PR include a completed AI explanation? | Yes / No |
| Could the on-call engineer explain the code before the incident? | Yes / No |
| Did any reviewer flag comprehension concerns during PR review? | Yes / No / Unknown |
| Was the code in a declared AI-Free Zone? | Yes / No |
| Was the failure mode a silent failure (no alarms)? | Yes / No |
| What was the blast radius (estimated users/records affected)? | [number] |

### Code Archaeology

If the code is not understood, work through it systematically — **with a person, not with AI**:

```
1. Read the failing function top to bottom, manually tracing data flow
2. Identify the specific line/condition that caused the failure
3. Understand why that condition was not caught in testing
4. Understand whether the bug is: logic error / missing edge case / integration assumption / 
   silent failure pattern / other
5. Document the finding in plain English before writing any fix
```

---

## Phase 3: Resolution

### Fix Authorization

| Scenario | Required Before Deploying Fix |
|----------|-------------------------------|
| Bug in AI code, fix is simple and understood | Lead review + 1 reviewer who understands both old and new code |
| Bug in AI code, fix is complex | Lead review + engineer who originally authored the failing code |
| Bug in AI-Free Zone | Tech Lead or senior engineer must author or co-author the fix |
| Data corruption involved | Lead + DBA/data owner sign-off before any data remediation |
| Security incident | Security lead sign-off required before deploying fix |

### Fix Standards

- The fix must be authored by someone who **understands the root cause**
- If the root cause is poorly understood code, fix the understanding before fixing the code
- Add regression tests that would have caught this specific failure
- The fix PR must include: what failed, why it failed, what the fix does, what was tested

---

## Phase 4: Post-Incident Review

The standard post-mortem template addition for AI-related incidents:

```markdown
## Cognitive Debt Section

### AI Code Assessment
- Was AI-generated code involved in this incident? [ ] Yes [ ] No [ ] Partial
- Was the failing code understood by the on-call team before the incident? [ ] Yes [ ] No
- Was the failure mode a silent failure? [ ] Yes [ ] No
- Did the PR template AI explanation accurately describe the failing behavior? [ ] Yes [ ] No [ ] No explanation present

### Contributing Factors
(Check all that apply)
[ ] Code was accepted without full author comprehension
[ ] Code was reviewed without reviewer comprehension
[ ] Code was in or adjacent to an AI-Free Zone without proper authorization
[ ] Silent error handling masked the failure until it cascaded
[ ] Test coverage did not include the failing edge case
[ ] MEMORY.md was missing relevant context that would have prevented the bug
[ ] Pattern inconsistency with the rest of the codebase contributed to the failure

### Required Actions
(Complete for every AI-related incident)
[ ] Add failing file/module to quarterly cognitive debt audit watchlist
[ ] Review and update MEMORY.md with missing context
[ ] Add failing edge case to regression test suite
[ ] Evaluate whether affected path should be added to AI-Free Zones
[ ] Schedule comprehension review for the affected module
[ ] Brief the team on the failure pattern to prevent recurrence

### AI-Free Zone Decision
Based on this incident, should any affected path be added to AI-Free Zones?
[ ] Yes — affected path: [path] — Reason: [reason]
[ ] No — Reason: [reason]
[ ] Deferred — pending further review at: [date]
```

---

## Phase 5: Prevention Loop

After every AI-related incident, the following actions are mandatory before the next sprint begins:

1. **Update MEMORY.md** — add any architectural context that would have prevented the bug
2. **Review AI-Free Zones** — consider whether the affected path meets the criteria
3. **Brief the team** — 15-minute team sync on what happened and the pattern to watch for
4. **Update test suite** — the exact failure scenario must have a regression test
5. **Audit similar code** — if the pattern is systemic, find other instances before they fail

---

## Severity Reference: AI Cognitive Debt Contribution Levels

Use these in incident severity classification and reporting:

| Level | Description | Example |
|-------|-------------|---------|
| **CD-1** | AI code caused complete data loss or security breach | Missing WHERE clause on DELETE; auth bypass |
| **CD-2** | AI code caused extended outage or significant data corruption | Silent failure corrupting records over days |
| **CD-3** | AI code caused partial outage or degraded service | Edge case crash affecting subset of users |
| **CD-4** | AI code involved but not primary cause; cognitive debt identified | Slow debugging due to incomprehensible code |
| **CD-5** | AI code involved, quickly resolved, no data impact | Minor bug in AI-generated boilerplate |

CD-1 and CD-2 incidents **require** a formal cognitive debt review of the affected module before it returns to production.

---

## Contacts & Escalation

| Situation | Escalate To |
|-----------|-------------|
| Data loss or corruption | [Data owner / DBA contact] |
| Security or auth failure | [Security lead contact] |
| Payment system involved | [Finance/payments owner contact] |
| Cannot find an engineer who understands the failing code | [Engineering Manager contact] |
| Incident involves AI-Free Zone violation | [Tech Lead contact] |

---
*Part of the [Cognitive Debt Prevention Kit](https://github.com/kesslernity/cognitive-debt-prevention-kit) by [Kesslernity](https://kesslernity.com)*
