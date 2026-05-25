# Skills.md

A small, tool-agnostic registry of reusable AI-agent skills.

Each skill lives in its own folder and uses `SKILL.md` as the canonical instruction file. Keep skills concise, procedural, and portable across agents whenever possible.

## Repository Layout

```text
<skill-name>/
|-- SKILL.md                 # Required: canonical skill instructions
|-- agents/openai.yaml       # Optional: Codex UI metadata
|-- scripts/                 # Optional: executable helpers
|-- references/              # Optional: detailed docs loaded only when needed
`-- assets/                  # Optional: templates, images, fonts, or other reusable files
```

Use `SKILL.md` for the core behavior. Put long examples, schemas, scripts, or templates in supporting folders and reference them from `SKILL.md`.

## Using These Skills

### OpenAI Codex

Install a skill globally by copying or symlinking it into your Codex skills directory:

```bash
git clone https://github.com/jdf-prog/Skills.md.git ~/Skills.md
mkdir -p ~/.codex/skills
ln -sfn ~/Skills.md/paper-writing-clarity ~/.codex/skills/paper-writing-clarity
```

Then invoke it naturally in Codex:

```text
Use $paper-writing-clarity to rewrite this intro.
```

Codex uses the `name` and `description` fields in `SKILL.md` to decide when a skill is relevant. The optional `agents/openai.yaml` file provides UI-facing metadata such as display name, short description, and default prompt.

### Claude Code

Claude Code also supports skills with a `SKILL.md` entrypoint. Install personal skills under `~/.claude/skills/`:

```bash
git clone https://github.com/jdf-prog/Skills.md.git ~/Skills.md
mkdir -p ~/.claude/skills
ln -sfn ~/Skills.md/paper-writing-clarity ~/.claude/skills/paper-writing-clarity
```

Or install a project-scoped skill inside a repo:

```bash
mkdir -p .claude/skills
ln -sfn ~/Skills.md/paper-writing-clarity .claude/skills/paper-writing-clarity
```

Invoke it directly with:

```text
/paper-writing-clarity rewrite this experiment section
```

Use `CLAUDE.md` for facts and preferences Claude should always load. Use skills for reusable procedures, checklists, workflows, and domain-specific actions that should load only when relevant.

### Other Models or Chat Interfaces

If a tool does not have native skill discovery, paste or attach the relevant `SKILL.md` and ask the model to follow it:

```text
Use the instructions in paper-writing-clarity/SKILL.md to review this paper section.
```

This loses automatic discovery, but keeps the skill reusable as a portable instruction artifact.

## Skill Index

| Skill | Best For | Trigger Examples | Codex | Claude Code |
| --- | --- | --- | --- | --- |
| [`paper-writing-clarity`](paper-writing-clarity/SKILL.md) | Academic paper writing, restructuring, LaTeX manuscript cleanup, experiment-section organization, terminology consistency, appendix triage, and figure/table support. | "Rewrite this intro", "organize the experiments", "make the paper clearer", "turn this discussion into a coherent section plan". | Use `$paper-writing-clarity` or rely on automatic matching from the description. | Use `/paper-writing-clarity` or rely on automatic matching from the description. |

## Maintenance Checklist

When adding a new skill:

1. Create `<skill-name>/SKILL.md` with YAML frontmatter containing `name` and `description`.
2. Keep the skill body focused. Move long examples, schemas, and templates into `references/`, `scripts/`, or `assets/`.
3. Add `agents/openai.yaml` when the skill should appear nicely in Codex UI.
4. Update the Skill Index table in this README.
5. Validate the skill when possible before pushing.

Prefer stable, lowercase, hyphenated skill names. Keep descriptions explicit about when the skill should trigger.

## References

- [Claude Code skills documentation](https://code.claude.com/docs/en/skills)
- [Claude Code memory and CLAUDE.md documentation](https://code.claude.com/docs/en/memory)
