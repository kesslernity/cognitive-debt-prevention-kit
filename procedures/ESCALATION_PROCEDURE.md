# 🔺 Escalation Procedure — Cognitive Debt Concerns
# Version: 1.0 | Review cycle: Quarterly
# Source: https://www.talk-nerdy-to-me.com/blog/cognitive-debt-ai-coding-hidden-cost

---

## Purpose

Cognitive debt compounds silently. Escalation is the mechanism that surfaces it before it becomes an incident. This procedure defines when to escalate, to whom, what to bring, and what outcome to expect.

The goal is to make it **safe and normal** to say "I don't understand this code" or "this codebase is becoming incomprehensible" — and to have a defined path forward when that happens.

---

## When to Escalate

### Individual Developer — Escalate When:

| Situation | Escalate To | Channel |
|-----------|-------------|---------|
| You're about to merge AI code you can't fully explain | Your tech lead | Direct message before merging |
| A reviewer is pressuring you to approve code you don't understand | Engineering manager | Private conversation |
| You've inherited a module where large portions are AI-generated and unexplained | Tech lead | Sprint standup or 1:1 |
| You're being asked to debug code in an AI-Free Zone and can't find anyone who wrote it | Tech lead | Immediate; same day |
| You notice a silent failure pattern in existing AI code that hasn't caused an incident yet | Tech lead | Within 24 hours |
| You find AI-generated code committed to an AI-Free Zone | Engineering manager | Same day |

### Tech Lead — Escalate When:

| Situation | Escalate To | Channel |
|-----------|-------------|---------|
| AI-generated code % exceeds 40% of recent changes without comprehension reviews | Engineering manager | Sprint review |
| MTTR on AI-heavy files is trending >2x non-AI files over 2+ sprints | Engineering manager | Sprint metrics review |
| Incident postmortem shows a pattern of "unclear why" attributions to AI code | Engineering manager | Post-incident debrief |
| A PR is being pushed through review despite failing the comprehension standard | Engineering manager | Direct, same day |
| A critical path module cannot be explained by any current team member | Engineering manager + relevant senior engineers | Emergency architecture review |
| A team member reports they feel pressure to accept AI code they don't understand | Engineering manager | Same day, private |

---

## Escalation Format

When escalating a cognitive debt concern, bring the following. A vague concern is harder to act on than a specific one.

**Template — Cognitive Debt Concern:**

```
Subject: Cognitive Debt Concern — [brief description]

WHAT I OBSERVED:
[Specific description: which file/module/PR, what the concern is, when you noticed it]

WHY IT'S A RISK:
[What could go wrong: incident risk, onboarding impact, maintainability, etc.]

WHAT I'VE TRIED:
[Steps already taken: asked the author, checked MEMORY.md, tried to trace the code, etc.]

WHAT I NEED:
[Specific ask: time for a comprehension review, decision on AI-Free Zone, blocked PR resolution, etc.]

URGENCY:
[ ] Blocking a current PR or deployment
[ ] Risk that should be addressed this sprint
[ ] Pattern to track in upcoming quarterly audit
```

---

## Response SLAs

Escalations must be acknowledged and have a path forward within these timeframes:

| Urgency | Acknowledgment | Resolution Path Defined |
|---------|---------------|------------------------|
| Blocking (PR, deployment) | 2 hours | Same day |
| Active risk (this sprint) | 24 hours | Within 3 business days |
| Pattern / trend | 48 hours | Addressed in next sprint planning |

---

## Escalation Outcomes

When a cognitive debt concern is escalated, the resolution should produce one or more of the following:

| Outcome | When It Applies |
|---------|----------------|
| **PR held** — AI explanation required before proceeding | Author cannot explain the code |
| **Comprehension review scheduled** — module reviewed as a team | Inherited module without adequate understanding |
| **AI-Free Zone added** — path added to MEMORY.md restrictions | Module is high-risk and repeatedly hard to understand |
| **Rewrite prioritized** — scheduled for next sprint or quarter | Module is critical and comprehension cannot be recovered through documentation |
| **MEMORY.md updated** — context documented to prevent recurrence | Missing context caused the confusion |
| **Team briefing scheduled** — pattern shared with whole team | Concern represents a pattern risk, not just an isolated case |
| **No action required** — concern reviewed and assessed as low risk | After assessment, risk is acceptable with current controls |

All escalations must produce a documented outcome — even if the outcome is "no action required" and why.

---

## Escalation Anti-Patterns

Things that should never happen in response to a cognitive debt escalation:

| Anti-Pattern | Why It's a Problem |
|-------------|-------------------|
| "We'll deal with it after launch" | This is exactly how cognitive debt accumulates into an incident |
| "Just approve it — we're under pressure" | Pressure is not a comprehension gate override |
| "Ask the AI to explain it" | AI explaining AI code is not human comprehension. It's recursive debt. |
| "It's fine — it passed the tests" | Tests passing and code being understood are independent properties |
| "The original author is gone — just leave it" | Undocumented code from departed authors is your highest-risk technical asset |
| Penalizing the engineer who raised the concern | Safe escalation requires psychological safety. Address this immediately. |

---

## Psychological Safety Commitment

Cognitive debt escalation only works if engineers feel safe raising concerns. This team commits to:

- **No blame** for raising a concern about code you inherited or didn't author
- **No judgment** for saying "I don't understand this"
- **Active appreciation** for engineers who surface cognitive debt before it becomes an incident
- **Process response** to concerns — every escalation gets a response, even if the answer is "accepted risk"

An engineer who says "I'm about to approve this but I don't really understand it" is doing the right thing. That should always be treated as a signal to slow down, not as a performance concern.

---
*Part of the [Cognitive Debt Prevention Kit](https://github.com/kesslernity/cognitive-debt-prevention-kit) by [Kesslernity](https://kesslernity.com)*
