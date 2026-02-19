<!-- .github/PULL_REQUEST_TEMPLATE.md -->
<!-- Drop this in your .github/ folder. GitHub picks it up automatically. -->

## Summary

<!-- What does this PR do? One paragraph max. -->

**Type of change:**
- [ ] Bug fix
- [ ] New feature
- [ ] Refactor (no behavior change)
- [ ] Performance improvement
- [ ] Infrastructure / config
- [ ] Documentation

**Linked issue / ticket:** [JIRA-XXX / GitHub #XXX]

---

## AI-Assisted Code Declaration

> If NO AI was used, check the box and skip this section.

- [ ] **No AI assistance used in this PR** — skip to the checklist below.

---

If AI was used, **you must complete all three fields**. This is a comprehension gate, not a formality.
If you can't answer these in your own words, you don't own this code yet.

### 1. What does this code do?
*(Your words — not the AI's summary, not a copy of the commit message)*

> 

### 2. Why this approach over the alternatives?
*(What did you consider? Why did you choose this direction?)*

> 

### 3. What edge cases did you verify?
*(List the scenarios you specifically tested or thought through — especially error paths)*

> 

---

## Testing

- [ ] Unit tests added / updated
- [ ] Integration tests added / updated (if applicable)
- [ ] Manually tested in: [ ] dev [ ] staging
- [ ] AI-generated code paths have **100% test coverage**

**How to test this PR locally:**
```
[steps to reproduce / test the change]
```

---

## Review Checklist (for Reviewers)

> Reviewers: if AI code is present, apply the comprehension standard too.
> If you can't explain what the code does after reading it, ask the author before approving.

- [ ] I understand what this code does — I can explain it to a teammate
- [ ] The AI explanation above matches what the code actually does
- [ ] No silent error handling (swallowed exceptions, default returns hiding failures)
- [ ] No hardcoded secrets, tokens, or credentials
- [ ] MEMORY.md updated if architecture or conventions changed
- [ ] PR is < 200 lines of meaningful change (excluding generated/lockfiles)
- [ ] Each logical concern is isolated (no multi-concern PRs)

---

## Blast Radius Assessment

*How contained is this change if something goes wrong?*

- **Affected services:** [list services / modules impacted]
- **Affected data:** [user data / financial data / none / etc.]
- **Rollback plan:** [feature flag / revert commit / migration rollback / etc.]
- **Monitoring:** [what metric/alert would fire if this breaks?]

---

## Notes for Reviewers

<!-- Anything specific you want reviewers to focus on, or context they need. -->
