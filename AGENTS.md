# Campaign workspace

- Read [the brand guide](Branding%20and%20references/brand-guidelines.md) before creating or changing creative work. Use approved decisions and assets; keep proposals and preferences explicitly labeled until the user approves them.
- When starting a campaign with an unconfigured brand, or when asked to explore its identity, follow the guide's **Brand discovery** process: begin with the user's idea and visual inspiration, then review a moodboard before establishing the identity. Resume from existing answers and approvals.
- Write shared files in English and match the user's language in conversation. Keep this campaign independent: do not copy another campaign's assets, credentials, history or creative decisions.
- Before any paid generation, state quantity, model and estimated cost and wait for explicit approval. Name the billing route; when both project API and connector are available, ask which to use. Record each real use according to the README's usage-record section.
- Keep real credentials exclusively in the ignored root `.env`. Create folders and records only when needed; maintain one source of truth for each responsibility.

## Video work

For video planning, storyboards, keyframes, clips, music, animation or editing, use the external video-factory workshop. Resolve `WORKSHOP` from the process environment's `VIDEO_FACTORY_HOME`; if unset or invalid, ask for its location.

Read `WORKSHOP/plugin/skills/video-factory/SKILL.md` and follow it before proceeding. Resolve specialist skills from `WORKSHOP/.agents/skills/` for Codex or `WORKSHOP/.claude/skills/` for Claude Code. Methodology and tools stay in the workshop; campaign outputs stay here.

Run workshop `bin/vf*` commands from this project root, using `.cmd` on Windows and `--project .` explicitly. Use [video-factory.json](video-factory.json) for destinations, approved inputs and deliverables. Follow the workshop's routing, review gates and checks rather than duplicating them here. If workshop writes are forbidden for the session, use read-only commands and stop before production creation or other workshop mutations.
