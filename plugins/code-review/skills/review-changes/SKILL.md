# Review Local Changes

Review staged and unstaged local changes in the current git repository.

## Steps

1. Gather the diff:
   - Run `git diff HEAD` to capture all local modifications (staged and unstaged)
   - Run `git status` to understand which files are new, modified, or deleted
   - For new (untracked) files that are relevant, read them directly

2. Understand context:
   - Read any files that are modified to understand surrounding code not visible in the diff
   - Check recent commit history (`git log --oneline -10`) to understand intent

3. Perform the review following [General Review Process](../review-files/SKILL.md#general-review-process)

4. Apply supplemental checks from [supplemental-checks/SKILL.md](../supplemental-checks/SKILL.md)

5. Present findings organized by file, ordered by severity (blocking issues first)
