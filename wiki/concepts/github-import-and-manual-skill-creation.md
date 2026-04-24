# GitHub Import and Manual Skill Creation

Beyond CLI-based installation, two additional paths are common:

## GitHub import from Cursor UI
- Uses Settings > Rules workflow to import a remote skill repository.
- Good for quick onboarding without command-line usage.
- Usually requires direct GitHub access and may require token handling for private repositories.

## Manual custom skill creation
- Create `.cursor/skills/<skill-name>/SKILL.md`.
- Author a clear YAML header and explicit step-by-step task guidance.
- Add templates/examples for repeatable generation quality.

Use this mode when workflows are domain-specific and not covered by public skill packs.

Related pages: [[concepts/skill-file-and-layout]], [[concepts/skill-usage-and-troubleshooting]]
