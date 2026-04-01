# code-review

Code review skill that supplements other review tools and plugins.

## Skills

### `review`
Review code from any source — local changes, a GitHub PR, or specific files. The skill determines what to gather based on context.

### `supplemental-checks`
Additional checks applied during every review. **Edit this file** to add domain-specific invariants, project conventions, and common mistake patterns.

## Setup

Edit `skills/supplemental-checks/SKILL.md` with your project-specific checks, then install:

```bash
/plugin install code-review@dug-claude-plugins
```

## Usage

```
Use the code-review:review skill
Use the code-review:review skill on PR #123
Use the code-review:review skill on src/foo.rb
```
