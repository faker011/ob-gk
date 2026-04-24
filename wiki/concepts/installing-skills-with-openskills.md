# Installing Skills with OpenSkills

`OpenSkills` is a CLI workflow for managing skill packs from GitHub or local paths.

Standard flow:
1. Ensure Node.js environment is available.
2. Run `openskills install <owner/repo>` (or local path).
3. Select desired skills in interactive mode (or use `-y` for all).
4. Run `openskills sync` to regenerate `AGENTS.md` and refresh discoverability.

Important operational details:
- Installation source is often GitHub, so network/proxy constraints matter.
- `--global` and `--universal` adjust installation scope/compatibility.
- `openskills update` is used for maintenance.
- Missing `sync` is a frequent reason skills appear "not detected".

This installation path is suited for teams that need repeatability, versioned updates, and multi-skill management.

Related pages: [[entities/OpenSkills]], [[entities/GitHub]], [[entities/AGENTS.md]]
