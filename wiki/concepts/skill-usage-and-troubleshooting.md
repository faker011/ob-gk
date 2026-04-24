# Skill Usage and Troubleshooting

Skill invocation can happen in two modes:
- Automatic: the agent chooses a skill from request context.
- Manual: user invokes by explicit skill command or direct instruction.

Troubleshooting checklist:
1. Validate exact filename: `SKILL.md`.
2. Verify folder path is under the correct project/global skill directory.
3. Confirm YAML frontmatter syntax is valid.
4. Ensure `name` and folder naming are consistent.
5. Run sync/refresh operation when using OpenSkills.
6. Re-check environment prerequisites (Node.js, network reachability for remote installs).

High-value operational habit: keep descriptions specific enough that auto-invocation can discriminate between similar skills.

Related pages: [[concepts/installing-skills-with-openskills]], [[concepts/skills-vs-rules]]
