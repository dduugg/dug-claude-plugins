# Review a Pull Request

Review a GitHub pull request — its diff, description, and context.

## Steps

1. Identify the PR:
   - If a PR number or URL was provided, use it
   - Otherwise use `gh pr view` to get the current branch's PR

2. Gather PR details:
   - `gh pr view <number> --json title,body,baseRefName,headRefName,files`
   - `gh pr diff <number>` to get the full diff

3. Understand context:
   - Read files that are modified to understand surrounding code not visible in the diff
   - Check the PR description for stated intent and test plan

4. Perform the review following [General Review Process](../review-files/SKILL.md#general-review-process)

5. Apply supplemental checks from [supplemental-checks/SKILL.md](../supplemental-checks/SKILL.md)

6. Present findings organized by file, ordered by severity (blocking issues first)

## Output Format

Summarize:
- **Overall assessment**: approve / request changes / comment
- **Blocking issues**: must be fixed before merge
- **Non-blocking suggestions**: improvements worth considering
- **Praise**: things done well (be specific)
