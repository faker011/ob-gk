# SKILL.md and Directory Layout

Each skill must be stored in a dedicated folder and include a file named exactly `SKILL.md` (uppercase). This naming is mandatory for reliable discovery.

Recommended structure:

```text
<project-root>/
  .cursor/
    skills/
      <skill-name-kebab-case>/
        SKILL.md
        (optional templates/resources)
```

Key constraints:
- Skill folder name uses `kebab-case`.
- YAML `name` in `SKILL.md` should match folder naming.
- `description` should clearly describe activation context.
- Optional resource files can be referenced by the skill instructions.

Common directories include project-level and global-level paths (Cursor-specific and Claude-compatible variants), but local project paths should be preferred for project-coupled workflows.

Related pages: [[entities/AGENTS.md]], [[concepts/installing-skills-with-openskills]]
