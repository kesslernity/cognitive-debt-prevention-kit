# 📜 AI Coding Tool Usage Guidelines
# Version: 1.0 | Review cycle: Quarterly
# Source: https://www.talk-nerdy-to-me.com/blog/cognitive-debt-ai-coding-hidden-cost

---

## Purpose

These guidelines define how, when, and under what conditions engineers on this team may use AI coding tools. They exist to capture the benefits of AI-assisted development while preventing the accumulation of cognitive debt — code that exists in production but is not understood by the team that maintains it.

These are **team agreements**, not suggestions.

---

## Scope

Applies to all AI coding tools including but not limited to: GitHub Copilot, Cursor, Claude Code, Amazon CodeWhisperer/Q, Tabnine, ChatGPT, and any other LLM-based tool used to generate, complete, or refactor code.

---

## 1. The Active vs. Passive Standard

Every engineer must apply the **Active Pattern** when working with AI tools.

| Pattern | Behavior | Outcome |
|---------|----------|---------|
| **Active** ✅ | Prompt → Read → Understand → Modify → Ship | Comprehension maintained |
| **Passive** ❌ | Prompt → Accept → Ship → Forget | Cognitive debt accumulates |

**What active use looks like in practice:**
- You write the function signature, types, and interface. AI fills the implementation.
- You define the test cases. AI generates the test bodies.
- You review the output against your mental model of the system, not just for syntax.
- You could explain the generated code to a colleague without reading it again.

**What passive use looks like (prohibited):**
- Accepting multi-function output without reading each function
- Using AI to generate architectural decisions you haven't made yourself
- Merging AI-generated code because it "looks right" without tracing the logic
- Generating code in unfamiliar domains without learning what was generated

---

## 2. Permitted Use Cases

### ✅ High-value, lower-risk uses
- Generating boilerplate (CRUD scaffolding, repetitive patterns you already understand)
- Writing test bodies for test cases you have defined
- Refactoring code you already understand (style, naming, structure)
- Generating documentation for code you wrote
- Explaining unfamiliar code (use AI to learn, not to ship)
- Drafting implementation from a design you have already reasoned through

### ⚠️ Permitted with mandatory comprehension review
- Algorithms or logic you didn't design yourself
- Any code touching a new domain (use AI to draft, then read deeply)
- Code that interacts with external APIs or services
- Any code >50 lines generated in a single output

### 🚫 Not permitted
- AI-generated code in **AI-Free Zones** (see MEMORY.md) without lead review and sign-off
- Generating and merging code you explicitly cannot explain
- Using AI to generate security-sensitive logic (auth, encryption, input validation) without expert review
- Generating database migration scripts without full human authorship and DBA review
- Using AI to resolve merge conflicts in logic-dense code

---

## 3. Tool Authorization

Before using any AI coding tool on this codebase:

1. **Check the Approved Tools List** (maintained in MEMORY.md or this document's Appendix)
2. **Complete team onboarding** — read MEMORY.md and this guidelines document
3. **Configure tool scope** — ensure the tool does not transmit proprietary code outside approved boundaries (check your company's data handling policy)
4. For new tools not on the approved list: raise in standup and get lead sign-off before using on production code

**Currently approved tools:**

| Tool | Approved For | Restrictions |
|------|-------------|--------------|
| [Tool name] | [Use cases] | [Restrictions] |
| [Tool name] | [Use cases] | [Restrictions] |

---

## 4. Disclosure Requirements

### In Pull Requests
All PRs containing AI-generated or AI-substantially-assisted code must:
- Check the AI disclosure box in the PR template
- Complete the three-question AI explanation section
- Tag the PR with the `ai-assisted` label (for metrics tracking)

Failure to disclose AI use is treated the same as any other process violation — address in 1:1, escalate on repeat.

### In Code Comments
For complex AI-generated functions, add a comment at the function level:

```python
# AI-assisted: drafted by [tool], reviewed and modified by [author], [date]
# Key logic verified: [brief note on what was specifically validated]
def process_payment(...):
    ...
```

This is not required for boilerplate or trivial AI assistance — use judgment. The bar is: "Would a future maintainer benefit from knowing this was AI-generated?"

### In Incident Postmortems
See `INCIDENT_RESPONSE_PROCEDURE.md` — AI origin must always be assessed as part of RCA.

---

## 5. Prohibited Behaviors

The following are explicitly prohibited and constitute violations of these guidelines:

| Prohibited Behavior | Why |
|--------------------|-----|
| Shipping AI code you cannot explain | Core definition of cognitive debt |
| Removing the AI explanation section from PR template | Circumvents comprehension gate |
| Marking AI code as human-written | Misrepresents review requirements |
| Using unapproved tools on production code | Data and security risk |
| Allowing AI to define architecture without human design | Leads to unexplainable systems |
| Using AI in declared AI-Free Zones without authorization | Unacceptable risk in critical paths |

---

## 6. Responsibilities

| Role | Responsibility |
|------|---------------|
| **Developer** | Apply the active pattern; complete PR disclosure; maintain MEMORY.md when patterns change |
| **Reviewer** | Verify AI explanation section; apply reviewer standard (see CODE_REVIEW_GUARDRAILS.md); not approve what they can't explain |
| **Tech Lead / Senior** | Model active AI use; hold PR standards; identify and flag cognitive debt accumulation |
| **Engineering Manager** | Enforce guidelines; run quarterly audits; track proxy metrics; update AI-Free Zones |
| **All** | Raise cognitive debt concerns early — in standup, in reviews, not in postmortems |

---

## 7. Guidelines Review and Updates

These guidelines are reviewed **quarterly** by the engineering lead and updated when:
- New AI tools are adopted or deprecated
- An incident is attributed to cognitive debt
- Team composition or codebase structure changes significantly
- Industry research materially changes the risk profile of AI-assisted coding

**Version history:**

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | [date] | [name] | Initial version |

---

## Appendix: Quick Reference Card

```
Before using AI → Am I using it actively or passively?
Before accepting → Can I pass the 3-question comprehension check?
Before merging → Is the PR explanation complete and accurate?
If unsure → Ask a senior dev, not the AI
If in doubt about a zone → Check MEMORY.md AI-Free Zones
If something breaks → Check INCIDENT_RESPONSE_PROCEDURE.md
```

---
*Part of the [Cognitive Debt Prevention Kit](https://github.com/kesslernity/cognitive-debt-prevention-kit) by [Kesslernity](https://kesslernity.com)*
