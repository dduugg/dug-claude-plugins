# Review Files

Review one or more specific files.

## Steps

1. Identify files to review:
   - Use files explicitly provided by the user
   - If none specified, ask which files to review

2. Read each file in full

3. Perform the review following the General Review Process below

4. Apply supplemental checks from [supplemental-checks/SKILL.md](../supplemental-checks/SKILL.md)

5. Present findings organized by file, ordered by severity (blocking issues first)

---

## General Review Process

Apply this process for all code review skills.

### Correctness
- Logic errors, off-by-one errors, incorrect conditions
- Unhandled edge cases (nil/null, empty collections, boundary values)
- Race conditions or incorrect assumptions about execution order
- Error handling: are errors caught, propagated, or swallowed appropriately?

### Security
- Injection vulnerabilities (SQL, shell, HTML/XSS)
- Insecure direct object references or missing authorization checks
- Sensitive data logged, exposed in errors, or stored insecurely
- Unsafe deserialization or use of user-controlled input

### Design & Maintainability
- Does the change do one thing clearly, or is it trying to do too much?
- Are abstractions at the right level — not too early, not too late?
- Are names (variables, functions, classes) clear and accurate?
- Is complexity justified, or is there a simpler approach?

### Test Coverage
- Are the important behaviors tested?
- Do tests assert outcomes or just that code runs?
- Are edge cases covered?

### Performance
- Obvious N+1 queries or redundant work in loops
- Unbounded operations on large datasets
- Unnecessary allocations in hot paths
