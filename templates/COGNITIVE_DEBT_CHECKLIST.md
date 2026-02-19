# 🧠 Cognitive Debt — Developer Checkpoint Card
# Run this BEFORE accepting any AI-generated block of code.
# Source: https://www.talk-nerdy-to-me.com/blog/cognitive-debt-ai-coding-hidden-cost

---

## ⚡ The 60-Second Pre-Accept Check

Answer these three questions before hitting accept on AI output.
**If any answer is "no" — stop. Understand first, then accept.**

### 1. Can I trace the data flow?
> Without reading line-by-line, can I explain what goes in, what transforms, and what comes out?

- [ ] Yes — I can narrate the flow
- [ ] No — I need to walk through it more carefully

### 2. Could I rewrite this from scratch?
> Not perfectly — but could I produce something functionally equivalent if the AI disappeared?

- [ ] Yes — this is within my competence zone
- [ ] No — I need to understand the approach before owning it in production

### 3. Would I catch a bug here at 2 AM?
> If this code breaks at 3 AM and I'm paged, can I debug it without looking up everything?

- [ ] Yes — I understand it well enough to diagnose under pressure
- [ ] No — I need more familiarity before this lands in production

---

## 🚦 Decision Tree

```
All 3 = YES?
  └─ ✅ Accept and move on

Any = NO?
  ├─ Ask AI to explain its approach step by step
  ├─ Ask AI for a simpler alternative you can fully own
  ├─ Rewrite the part you don't understand yourself
  └─ Add inline comments documenting the why — if you can't write them, you don't understand
```

---

## 🔬 Code Quality Sniff Test

Run these eyes-on checks before submitting for review:

**Error Handling**
- [ ] No bare `except` / `catch` that swallows errors silently
- [ ] No `return null` / `return {}` hiding failures from callers
- [ ] No TODO comments left from AI output (e.g., "handle error here")

**Security**
- [ ] No secrets, tokens, or credentials hardcoded
- [ ] Input is validated before use (not just assumed clean)
- [ ] SQL/queries use parameterized inputs — no string interpolation

**Consistency with Codebase**
- [ ] Follows naming conventions in MEMORY.md
- [ ] Uses established error classes / patterns (not new ad-hoc ones)
- [ ] Imports only from approved layers (no layer-skipping)
- [ ] Matches existing code style (AI often invents new patterns — don't let it)

**Scope Control**
- [ ] This change does one thing
- [ ] PR is under 200 meaningful lines
- [ ] If it's bigger, it's been broken into reviewable chunks

---

## 🧭 Pairing Pattern (For AI-Assisted Sessions)

Use this workflow when coding with AI agents:

```
YOU write:          → Function signatures
                    → Interface / type definitions  
                    → The approach / algorithm sketch
                    → Test cases for expected behavior

AI writes:          → Implementation body
                    → Boilerplate
                    → Repetitive patterns

YOU verify:         → Run the tests YOU defined
                    → Trace the logic manually
                    → Update MEMORY.md if patterns changed
```

**Never let the AI define the architecture. You steer. AI fills.**

---

## 📊 Personal Cognitive Debt Tracker

Use this weekly to spot drift before it compounds:

| Metric | This Week | Last Week | Trend |
|--------|-----------|-----------|-------|
| PRs where I couldn't explain all AI code | | | |
| Times I shipped code I didn't fully understand | | | |
| Bugs/incidents tied to AI-generated code I own | | | |
| MEMORY.md updates made | | | |

**Red flag:** If row 1 or 2 is non-zero two weeks in a row, slow down and schedule a comprehension review session.

---

## 🆘 If You're Already In Debt

Signs you've accumulated cognitive debt:
- You're afraid to touch certain files because you don't know what they do
- Incident postmortems have "unclear why" entries about AI-generated code
- New engineers ask you questions about code you can't answer

**Recovery steps:**
1. Identify the high-risk / high-debt files (usually critical paths + AI-heavy PRs)
2. Schedule a "comprehension sprint" — no new features, just reading and documenting
3. Add inline comments explaining WHY (not what — the code shows what)
4. Update MEMORY.md with everything you re-learn
5. Consider a targeted rewrite of the highest-risk sections

---

*Cognitive debt compounds silently. The best time to prevent it is before you accept the code. The second best time is now.*

---
*Part of the [Cognitive Debt Prevention Kit](https://github.com/kesslernity/cognitive-debt-prevention-kit) by [Kesslernity](https://kesslernity.com)*
