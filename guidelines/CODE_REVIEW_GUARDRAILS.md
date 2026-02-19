# 🔍 Code Review Guardrails — AI-Generated Code
# Version: 1.0 | Review cycle: Quarterly
# Source: https://www.talk-nerdy-to-me.com/blog/cognitive-debt-ai-coding-hidden-cost

---

## Why AI Code Needs Different Review Standards

AI-generated code has a distinct failure signature. It is:

- **Syntactically clean** — it passes linters and looks professional
- **Logically subtle** — errors hide in edge cases, not obvious mistakes
- **Idiomatically foreign** — it often doesn't match your codebase conventions
- **Confidently wrong** — it does not signal uncertainty; broken code looks identical to correct code

Standard code review practices were designed for human-written code where the author understands what they wrote. AI code review requires an additional layer: **verifying the author's comprehension**, not just the code's correctness.

---

## Part 1: Reviewer Prerequisites

Before reviewing any PR containing AI-generated code, confirm:

- [ ] You have read and understood the PR description's AI explanation section
- [ ] The explanation was written in the author's own words (not the AI's summary)
- [ ] The PR is scoped to a single logical concern
- [ ] The PR is under 200 lines of meaningful change

**If the AI explanation is missing or vague:** Request it before reviewing any code. A PR without a completed AI explanation section is not review-ready, regardless of code quality.

---

## Part 2: The Review Layers

### Layer 1 — Comprehension Verification

This is the layer unique to AI code review.

Ask yourself: **Does the author demonstrably understand what they submitted?**

Check the AI explanation section for:

| Signal | Healthy | Red Flag |
|--------|---------|----------|
| Language | Author's voice, specific | Sounds like AI output |
| Alternatives considered | Yes, even briefly | "This is the best approach" with no reasoning |
| Edge cases | Specific and tested | Generic ("handles errors") |
| Implementation rationale | Explains the why | Only describes the what |

If the explanation doesn't satisfy this check, leave a review comment requesting clarification before proceeding. **Do not approve code the author cannot explain.**

---

### Layer 2 — Silent Failure Patterns

AI has a strong tendency to produce code that fails silently. Look explicitly for:

**Swallowed exceptions:**
```python
# ❌ AI frequently generates this
try:
    result = external_api.call()
except Exception:
    pass  # or: return None / return {} / return []

# ✅ What it should look like
try:
    result = external_api.call()
except SpecificError as e:
    logger.error("API call failed: %s", e)
    raise  # or handle explicitly with a defined fallback
```

**Default returns masking failures:**
```typescript
// ❌ Caller has no idea if this succeeded or returned a default
function getUserConfig(userId: string): Config {
  try {
    return fetchConfig(userId);
  } catch {
    return DEFAULT_CONFIG; // silent fallback — caller won't know
  }
}

// ✅ Explicit failure signaling
function getUserConfig(userId: string): Config | null {
  try {
    return fetchConfig(userId);
  } catch (err) {
    logger.error({ userId, err }, "Failed to fetch user config");
    return null; // caller must handle null explicitly
  }
}
```

**AI-generated TODO/FIXME comments:**
```python
# ❌ These are cognitive debt time bombs
# TODO: handle edge case here
# FIXME: this might not work for all cases
# Note: assuming input is valid (AI left this comment)
```
Any TODO left by AI output that isn't tracked in a ticket is a rejection reason. Either address it or create a tracked ticket before merging.

---

### Layer 3 — Codebase Consistency

AI generates code in its own patterns. Your codebase has established patterns. Gaps between them are future maintenance burdens.

Check for:

**Pattern violations:**
- [ ] Uses approved error class/handling approach (see MEMORY.md)
- [ ] Queries go through the correct data access layer (see MEMORY.md)
- [ ] Naming conventions match the codebase (see MEMORY.md)
- [ ] No new abstractions or utilities invented when existing ones should be used

**Idiom drift:**
```typescript
// ❌ AI might generate this (technically correct, idiomatically wrong for your codebase)
const result = Object.assign({}, defaults, overrides);

// ✅ If your codebase uses this pattern
const result = { ...defaults, ...overrides };
```

**Import/dependency hygiene:**
- [ ] No new dependencies introduced without discussion
- [ ] No imports from layers that shouldn't have access (layer violations)
- [ ] No unused imports left from AI generation
- [ ] No dead code paths (AI frequently generates unreachable code)

---

### Layer 4 — Security Review (Mandatory for Sensitive Paths)

For any code touching auth, user input, external APIs, or data persistence:

**Input handling:**
- [ ] All external inputs are validated before use — never assumed clean
- [ ] No SQL string interpolation — only parameterized queries
- [ ] No shell command construction from user input
- [ ] File paths sanitized if derived from user input

**Credential hygiene:**
- [ ] No hardcoded secrets, tokens, or API keys
- [ ] No secrets in log statements
- [ ] No secrets in error messages returned to clients

**Data exposure:**
- [ ] Response objects don't leak internal fields (check serialization)
- [ ] Error messages don't expose stack traces or internal structure to clients
- [ ] PII is not logged

---

### Layer 5 — Test Coverage of AI Paths

AI-generated code must be tested. AI-written tests for AI-generated code require extra scrutiny — the AI may have written tests that only cover the happy path it generated.

**Coverage requirements:**
- [ ] Every AI-generated function has at least one test
- [ ] Error/exception paths are explicitly tested (not just assumed handled)
- [ ] Edge cases mentioned in the PR explanation have corresponding tests
- [ ] No test that only asserts the happy path for a function with meaningful error behavior

**Test quality signals:**
```python
# ❌ AI frequently writes tests like this — only validates happy path
def test_process_order():
    result = process_order(valid_order)
    assert result.status == "success"

# ✅ What complete coverage looks like
def test_process_order_success():
    result = process_order(valid_order)
    assert result.status == "success"

def test_process_order_invalid_item():
    with pytest.raises(InvalidItemError):
        process_order(order_with_invalid_item)

def test_process_order_payment_failure():
    result = process_order(order_with_failing_payment)
    assert result.status == "payment_failed"
    assert result.order_id is not None  # order preserved for retry
```

---

## Part 3: Review Decision Framework

```
Read PR description AI explanation
        │
        ├─ Missing or clearly AI-written?
        │         └─ Request before reviewing. Not review-ready.
        │
        └─ Present and credible?
                  │
                  ├─ Review code against Layers 2-5
                  │
                  ├─ Found silent failures or pattern violations?
                  │         └─ Request changes. Explain why specifically.
                  │
                  ├─ Security concern in a sensitive path?
                  │         └─ Flag for senior/security review before approving.
                  │
                  ├─ In or near an AI-Free Zone?
                  │         └─ Require lead sign-off, not just peer review.
                  │
                  └─ All layers pass?
                            └─ Approve with confidence.
```

---

## Part 4: Reviewer Comments — Communication Standards

When requesting changes on AI-generated code, be specific about what needs to change and why. Vague comments cause iteration loops.

**Good review comment:**
> "This catch block swallows the `DatabaseConnectionError` without logging or re-throwing it. If the DB goes down, callers will receive an empty list and have no visibility into the failure. Can you either re-throw after logging, or surface this as a typed error the caller can handle?"

**Weak review comment:**
> "Better error handling needed"

**When you can't explain something yourself:**
> "I'm not following the logic in `calculateAdjustedRate()` — the comment says it handles edge cases but I'm not clear on which ones. Can you add a comment or explain in the PR? I want to understand this before approving."

Saying "I don't understand this" in a review is not a weakness. It's cognitive debt prevention.

---

## Part 5: Reviewer Self-Assessment

After completing a review of AI-assisted code, ask yourself:

- Could I explain what this code does to an on-call engineer at 3 AM?
- If this code broke in production, could I diagnose it without re-reading it entirely?
- Do I feel comfortable saying "I reviewed this and I own my approval"?

If any answer is "no," do not approve. Ask more questions or request changes that make the code explainable.

**Your approval is not a rubber stamp. It's a statement of shared ownership.**

---
*Part of the [Cognitive Debt Prevention Kit](https://github.com/kesslernity/cognitive-debt-prevention-kit) by [Kesslernity](https://kesslernity.com)*
