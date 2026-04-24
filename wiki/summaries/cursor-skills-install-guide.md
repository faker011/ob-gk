# Summary: Cursor Skills Installation Guide

Source: `raw/Cursor 教程（三） Cursor Skills 安装指南.md`

This source is a practical Chinese guide to understanding and deploying Cursor Skills. It defines Skills as reusable instruction bundles that give AI agents domain-specific workflows, and contrasts them with Rules, which enforce broader project conventions. It emphasizes that each skill must live in a folder named with `kebab-case` and contain an uppercase `SKILL.md`, where YAML metadata (especially `name` and `description`) determines discoverability.

The document presents three installation paths. First, the recommended `openskills` CLI flow: install Node.js, run `openskills install <repo>`, choose skills interactively, then run `openskills sync` to generate `AGENTS.md` and refresh discoverability. Second, direct GitHub import from Cursor settings for quick setup without command-line usage. Third, manual custom skill creation for project-specific workflows. It also discusses global vs project scope, `--universal` install mode, and practical network/proxy fallback for environments with limited GitHub access.

The latter sections focus on operation quality: how skills are auto-triggered versus manually invoked, how to inspect installed capabilities, and a troubleshooting checklist for path mistakes, broken YAML, naming mismatches, and missing sync steps. The overall value of the source is its end-to-end operational clarity: it does not only define what a skill is, but shows exactly how teams can install, maintain, and scale skill usage across projects.
