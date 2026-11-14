# Lauren Tan (unofficial distillation)

This repository is a skill that speaks as Lauren Tan (poteto), in first person, from her public talks, writing, and posts. It is not Lauren Tan, and it is not endorsed by her.

## What it is

An unofficial persona skill. Once loaded, an agent answers as Lauren Tan, using the voice, opinions, and boundaries in this repo:

- `ENTRY.md` — who she is, how to answer, and what to say if asked whether this is really her
- `VOICE.md` — how she sounds, plus exact quotes
- `OPINIONS.md` — positions she has taken in public
- `BOUNDARIES.md` — limits she has actually stated

The material comes from public sources: talks, podcasts, articles, blog posts, GitHub READMEs, and a sample of her posts on X. It is a distillation of public speech, not a private or official channel.

## How to add this repo as a skill

The loader lives at `skills/lauren-tan/SKILL.md`. It fetches the four files above from this repository (GitHub raw, with a jsDelivr fallback).

1. Clone the repository:

   ```bash
   git clone https://github.com/charlescstpierr/lauren-tan.git
   ```

2. Copy or link the skill folder into your agent's skills directory, for example:

   - Cursor: `~/.cursor/skills/lauren-tan` or `<project>/.cursor/skills/lauren-tan`
   - Claude Code / Agent Skills: `.claude/skills/lauren-tan` or `~/.claude/skills/lauren-tan`

   ```bash
   mkdir -p ~/.cursor/skills
   cp -R lauren-tan/skills/lauren-tan ~/.cursor/skills/lauren-tan
   ```

   If your tool can install a skill directly from a GitHub repository, point it at `https://github.com/charlescstpierr/lauren-tan`.

3. After that, ask the agent to talk as Lauren Tan (poteto). It should load this skill and answer in character.
