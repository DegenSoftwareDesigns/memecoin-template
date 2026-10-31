# memecoin-template

Minimal shared workspace for a memecoin campaign. Each campaign starts with its own identity and approved references.

## Structure

| Path | Responsibility |
| --- | --- |
| [AGENTS.md](AGENTS.md) | Agent instructions and workshop handoff |
| [Branding and references/brand-guidelines.md](Branding%20and%20references/brand-guidelines.md) | Brand decisions and approval status |
| `Branding and references/Brand assets/` | Reusable assets directly in this folder, e.g. `avatar.png`, `banner-01.png`, `wordmark.png` |
| `Branding and references/Character/` | Character references |
| `Images/` | Posts and illustrations |
| `Videos/` | Video deliverables and production materials |
| [video-factory.json](video-factory.json) | Video destinations, approved inputs and deliverable contract |
| [.env.example](.env.example) | Empty provider key names; copy to the ignored root `.env` |
| [.gitignore](.gitignore) | Secret and local configuration exclusions |

The four `.gitkeep` files preserve empty folders in Git; remove each when that folder gains content. Create other folders only when work needs them.

## Start a campaign

1. On GitHub, select **Use this template > Create a new repository**, then clone the new repository into a uniquely named campaign folder. See [GitHub's template instructions](https://docs.github.com/en/repositories/creating-and-managing-repositories/creating-a-repository-from-a-template).
2. Open the repository in your LLM and use the starter prompt below. Follow **Brand discovery** in the brand guide, beginning with your idea and inspiration images. Add assets as they are approved and list only approved input paths in `video-factory.json`'s `references` array.
3. Replace this README's title with the campaign name. The workshop derives the project identity from the root folder name; keep that name unique across campaigns on each machine, or set a unique shared `name` and `slug` in the manifest.
4. If using provider APIs, copy `.env.example` to `.env` at this repository's root and fill only the keys needed. All real credentials belong exclusively in that ignored root file. Connectors instead use each person's signed-in account.
5. For video work, configure the external workshop below. Image-only work needs no workshop runtime installed in this repository.

Shared files use English. Conversation follows the user's language.

### Start with your LLM

If your assistant does not automatically read `AGENTS.md`, explicitly ask it to read that file and the brand guide. Give it access to those files or paste their contents. Attach inspiration images in the conversation; you do not need an existing logo, character or finished brief.

```text
Read AGENTS.md and Branding and references/brand-guidelines.md.
Help me discover this campaign's brand, starting with the Brand discovery process.
Ask me about the idea and invite me to share look-and-feel inspiration images.
Use my answers to propose and review a visual moodboard with me before defining
the identity or producing campaign assets. Keep undecided details open.
```

## Video workshop setup

Requirements: Git, an agent that reads `AGENTS.md`, and, for video work, a separate configured video-factory checkout with its dependencies installed according to its own README. This repository installs no tools.

Each teammate sets `VIDEO_FACTORY_HOME` to their own workshop folder in the process environment before starting the agent. It is an operating-system variable: putting it in the project `.env` does not configure workshop discovery.

PowerShell (current session and future sessions):

```powershell
$env:VIDEO_FACTORY_HOME = '<absolute path to your video-factory checkout>'
[Environment]::SetEnvironmentVariable('VIDEO_FACTORY_HOME', $env:VIDEO_FACTORY_HOME, 'User')
```

Bash (persist the export in your own shell profile if desired):

```bash
export VIDEO_FACTORY_HOME="<absolute path to your video-factory checkout>"
```

Restart the agent after changing its environment. Keep personal paths out of shared files. Read `plugin/skills/video-factory/SKILL.md` inside that workshop for the workflow; its README owns workshop installation and optional Claude Code plugin setup. Codex uses the entry file through `AGENTS.md`.

From this project's root, verify routing without starting a production:

```powershell
& "$env:VIDEO_FACTORY_HOME\bin\vf.cmd" paths routing-check --project .
& "$env:VIDEO_FACTORY_HOME\bin\vf-run.cmd" --project . --list
```

```bash
"$VIDEO_FACTORY_HOME/bin/vf" paths routing-check --project .
"$VIDEO_FACTORY_HOME/bin/vf-run" --project . --list
```

`paths` is read-only. `--list` shows the environment file location and configured key names, never values. Empty values are omitted. Confirm it points at this project's `.env`; a missing file is normal before API setup. Run keyed tools through `vf-run` with this project selected and verify the required project key exists before invoking them: missing keys can otherwise fall back to the inherited environment.

The manifest resolves production materials to `Videos/{production}` and final MP4 files to its `final/` subfolder; these folders are created only when needed. It requires at least one final MP4 and leaves planning outputs and aspect ratio to the approved brief and workshop. Adjust the contract if a production needs another delivery format. The workshop's `check` validates declared files, not creative approval or media quality.

The workshop owns methodology and runtime state. Starting a production with `vf new` writes its local registry and `.work/` files in the external workshop; this template does not create those records. If that checkout must remain read-only, stop before commands that write there.

## Usage records

Create root `api-usage.csv` only when recording the first actual API or connector use. The manifest already points to that future record; no placeholder log is needed. Use one row per real request, including date, production or asset, provider, route (API/connector), model, quantity, estimated cost, actual cost when known, currency and approval reference. Mark unknown actual costs as pending rather than zero. Record the explicit approval in the same row, without credentials or personal paths.

## Publish this template after review

Review `git status --short`, open each new file in your editor, and run `git status --short --ignored` before the first commit. Confirm `.env` is ignored with `git check-ignore .env` and inspect the files selected for sharing. Keep campaign assets and real usage out of the template itself.

After approval, commit the scaffold, create an empty GitHub repository, add its remote and push `main`. A repository administrator then enables **Settings > General > Template repository**. This is a GitHub setting, not a local configuration file; see [GitHub's template setup](https://docs.github.com/en/repositories/creating-and-managing-repositories/creating-a-template-repository). Teammates can then follow the campaign steps above.
