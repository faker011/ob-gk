# Skills vs Rules

Skills and Rules solve different layers of agent behavior:

- Skills answer "how to execute a specific task."
- Rules answer "what project-wide conventions always apply."

Typical split:
- Skills: code review flow, API generation workflow, test-writing procedure.
- Rules: TypeScript strictness, naming conventions, folder architecture.

Practical guidance:
1. Put repeatable, task-scoped procedures into Skills.
2. Put broad, persistent standards into Rules.
3. Keep overlaps minimal to avoid contradictory instruction priority.

Related pages: [[concepts/what-are-cursor-skills]], [[concepts/skill-usage-and-troubleshooting]]
