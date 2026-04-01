# Claude Code Plugins Monorepo

This repository contains Claude Code plugins for `dug-claude-plugins`.

## Repository Structure

```
plugins/
└── {plugin-name}/    # Your plugins go here
```

## Plugin Internal Structure

Each plugin follows this structure:

```
plugins/{name}/
├── .claude-plugin/
│   └── plugin.json       # Manifest with name, description (NO version)
├── commands/
│   └── {command}.md      # FLAT files: commands/foo.md
├── skills/
│   └── {skill}/
│       └── SKILL.md      # NESTED: skills/foo/SKILL.md
├── hooks/
│   └── {hook-type}.{ext} # Hook scripts
└── README.md
```

**Critical distinction:**
- **Commands**: Flat files → `commands/{name}.md`
- **Skills**: Nested directories → `skills/{name}/SKILL.md`

## Versioning

Versions live in `.claude-plugin/marketplace.json` only (not in plugin.json files).

Commits must use conventional format: `type(scope): description`

```bash
feat(plugin): add feature    # → minor bump
fix(plugin): fix bug         # → patch bump
chore: update deps           # → no bump
```

## Development vs Installation

### Local Development

Changes to local source require reinstall to take effect:

```bash
/plugin uninstall {plugin}@dug-claude-plugins
/plugin install {plugin}@dug-claude-plugins
# Restart Claude Code
```

### Referencing Files in Skills

Use standard markdown links in SKILL.md files:

```markdown
# Correct
See [references/index.md](references/index.md) for details.

# Wrong - @ imports only work in CLAUDE.md, not SKILL.md
See `@references/index.md` for details.
```
