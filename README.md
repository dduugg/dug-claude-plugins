# dug-claude-plugins

Personal plugin marketplace for Claude Code.

## Repository Structure

```
dug-claude-plugins/
├── .claude-plugin/
│   ├── plugin.json           # Root marketplace metadata
│   └── marketplace.json      # Plugin registry
├── plugins/
│   └── {plugin-name}/
│       ├── .claude-plugin/
│       │   └── plugin.json
│       ├── skills/
│       │   └── {skill-name}/
│       │       └── SKILL.md
│       ├── commands/          # Optional
│       │   └── {command}.md
│       ├── hooks/             # Optional
│       └── README.md
└── scripts/
```

## Installation

### Add the Marketplace

```bash
/plugin marketplace add dduugg/dug-claude-plugins
```

### Install a Plugin

```bash
/plugin install <plugin-name>@dug-claude-plugins
```

## Development

### Plugin Structure

Each plugin follows this layout:

```
plugins/{plugin-name}/
├── .claude-plugin/
│   └── plugin.json
├── skills/
│   └── {skill-name}/
│       └── SKILL.md
├── commands/          # Optional - flat files: commands/{name}.md
└── hooks/             # Optional
```

**Note:**
- **Commands**: Flat files → `commands/{name}.md`
- **Skills**: Nested directories → `skills/{name}/SKILL.md`

### Versioning

Versions live in `.claude-plugin/marketplace.json` only (not in individual `plugin.json` files).

Commits use conventional format: `type(scope): description`

```bash
feat(my-plugin): add new skill    # → minor bump
fix(my-plugin): fix edge case     # → patch bump
chore: update deps                # → no bump
```

Use `./scripts/bump-version.sh` to bump plugin versions.

### Testing

```bash
./bin/test-claude              # Setup isolated config and run claude
./bin/test-claude --clean      # Reset test config
```

## License

MIT
