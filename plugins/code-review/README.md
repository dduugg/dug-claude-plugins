# code-review

Code review skills that supplement other review tools and plugins.

## Skills

### `review-changes`
Review staged and unstaged local git changes.

### `review-pr`
Review a GitHub pull request by number or URL.

### `review-files`
Review one or more specific files.

### `supplemental-checks`
Additional checks applied by all review skills. **Edit this file** to add your own domain-specific invariants, project conventions, and common mistake patterns.

## Setup

1. Edit `skills/supplemental-checks/SKILL.md` with your project-specific checks
2. Install the plugin:
   ```bash
   /plugin install code-review@dug-claude-plugins
   ```

## Usage

```
Use the code-review:review-changes skill
Use the code-review:review-pr skill on PR #123
Use the code-review:review-files skill on src/foo.rb
```
