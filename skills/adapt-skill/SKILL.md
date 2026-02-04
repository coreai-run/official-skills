---
name: adapt-skill
description: Convert existing Claude Code skills to CORE AI-compatible format
---

# Adapt Skill

Convert existing skills with hardcoded values into CORE AI-compatible skills that use configuration injection.

## Usage

```
/adapt-skill <source>
```

Where `<source>` is either:
- A URL to a SKILL.md file (GitHub, raw URL, etc.)
- A local file path to a SKILL.md file

## Examples

```
/adapt-skill https://github.com/user/repo/blob/main/skills/thumbnail/SKILL.md
/adapt-skill ~/.claude/skills/my-old-skill/SKILL.md
/adapt-skill /path/to/downloaded/SKILL.md
```

## What I Will Do

### Step 1: Read the Original Skill

I will fetch and read the skill from the provided source.

### Step 2: Analyze for Hardcoded Values

I will identify:
- **Personal paths**: Directories like `/Users/name/`, `~/Projects/specific/`
- **Brand colors**: Hex codes, RGB values
- **Font specifications**: Font families, weights, sizes
- **API configurations**: Model names, API endpoints, quality settings
- **Project/channel names**: Specific brand names, channel names
- **URLs**: Website URLs, social media links
- **Credentials references**: API key locations (not the keys themselves)
- **Output configurations**: File formats, dimensions, quality settings

### Step 3: Generate Adapted SKILL.md

I will create a new SKILL.md that:
- Removes all hardcoded values
- Adds `!`coreai config show <skill-name>`` for config injection
- Preserves all original instructions and logic
- References configuration fields instead of hardcoded values

### Step 4: Generate defaults.yaml

I will create a defaults.yaml with:
- All extracted values organized into logical groups
- Generic defaults (black/white colors, standard paths)
- Comments explaining each configuration option
- The original hardcoded values as reference comments

### Step 5: Ask for Profile Configuration

I will ask you:
1. Which profile should I configure with the original values?
2. Do you want to modify any values before saving?

### Step 6: Create the Files

I will create:
- `~/.coreai/skills/<skill-name>/SKILL.md`
- `~/.coreai/skills/<skill-name>/defaults.yaml`
- `~/.coreai/profiles/<your-profile>/<skill-name>.yaml` (if you specify a profile)

### Step 7: Link to Claude Code

I will create the symlink:
```bash
ln -s ~/.coreai/skills/<skill-name> ~/.claude/skills/<skill-name>
```

## Output Format

After adaptation, I will provide:

1. **Summary of changes**: What was hardcoded and how it was extracted
2. **The adapted SKILL.md**: Full content for review
3. **The defaults.yaml**: Full content for review
4. **Profile override**: Your specific configuration
5. **Testing instructions**: How to verify the adaptation

## Configuration Categories

I organize extracted values into these standard categories:

```yaml
# AI/API settings
model: <model-name>
quality: <quality-setting>
api:
  endpoint: <url>
  version: <version>

# Visual style
style:
  colors:
    primary: <color>
    secondary: <color>
    accent: <color>
    background: <color>
    text: <color>
  typography:
    font_family: <font>
    font_weight: <weight>
    font_size: <size>
  dimensions:
    width: <width>
    height: <height>
    aspect_ratio: <ratio>

# Output settings
output:
  directory: <path>
  format: <format>
  quality: <quality>
  filename_pattern: <pattern>

# Platform/brand settings
platform:
  name: <name>
  description: <description>
  url: <url>

# Content settings
content:
  language: <language>
  tone: <tone>
  max_length: <length>
```

## Notes

- I preserve the original skill's logic and instructions
- I only extract truly variable values, not constants
- I create sensible generic defaults, not empty placeholders
- I ask for confirmation before creating any files
- I explain each change so you understand the adaptation

## Limitations

- I cannot access private repositories without proper authentication
- I cannot extract values from binary files or images
- I preserve but don't modify tool dependencies
- Complex conditional logic may need manual adjustment

## After Adaptation

Test the adapted skill:

```bash
# Verify config
coreai config show <skill-name>

# Test in Claude Code
/skill-name <test prompt>
```

If issues occur, check:
1. Skill name matches across all files
2. Profile is active: `coreai profile current`
3. Symlink exists: `ls -la ~/.claude/skills/<skill-name>`
