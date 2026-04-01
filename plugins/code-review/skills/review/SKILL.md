# Code Review

Review code from any source: local changes, a pull request, or specific files.

## Gathering Code

Determine what to review based on context:

- **Local changes**: `git diff HEAD` for all modifications; `git status` for new/deleted files; read new untracked files directly
- **Pull request**: `gh pr view <number> --json title,body,files` then `gh pr diff <number>`; if no number given, use `gh pr view` for the current branch
- **Specific files**: read each file provided; if none specified, ask

In all cases, read surrounding code in modified files as needed to understand context.

## Review Checklist

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

## Supplemental Checks

Apply all checks from [supplemental-checks/SKILL.md](../supplemental-checks/SKILL.md).

## Output

Present findings ordered by severity:
- **Blocking issues**: must be fixed
- **Suggestions**: improvements worth considering
- **Praise**: things done well (be specific)

For PRs, conclude with an overall assessment: approve / request changes / comment.
