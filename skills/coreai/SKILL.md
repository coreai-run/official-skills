---
name: coreai
description: Use when user asks about profiles, configuration, or skill management in CORE AI
---

# CORE AI

CORE AI manages profiles, configuration injection, and shareable skills for Claude Code.

## When to Use

- User asks about profiles or switching contexts
- User wants to install, search, or manage skills
- User needs configuration for a skill
- User mentions "coreai" commands

## Current Profile

!`coreai profile current`

## Available Commands

!`coreai --help`

### Profile Commands

!`coreai profile --help`

### Skill Commands

!`coreai skill --help`

### Config Commands

!`coreai config --help`

## Directory Structure

```
~/.coreai/
├── profiles/          # Profile configurations
├── skills/            # Installed skills
└── config.yaml        # Global config
```

## Examples

```bash
# Switch profile
coreai profile use work

# Install a skill from registry
coreai skill install <name> --link

# Search available skills
coreai skill search

# View skill config
coreai config show <skill-name>
```

## Troubleshooting

If a command fails, run it directly to see the error:
```bash
coreai <command> --help
```
