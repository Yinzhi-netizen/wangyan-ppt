# Wangyan Installation

Use this reference for a fresh installation or a missing sibling engine.

## 1. Install both skills

Use Codex's built-in `$skill-installer` with:

| Option | Value |
|---|---|
| Repository | `Yinzhi-netizen/wangyan-ppt` |
| Ref | `main` |
| Paths | `skills/wangyan-ppt` and `skills/ppt-master` |
| Destination | One shared user-level skills directory; prefer `~/.agents/skills` |

When using the bundled installer's script, pass both paths in a single
`--path` argument and an absolute expanded `--dest` path. Both folders must be
siblings. If either destination already exists, stop and ask before replacement;
do not rename only one folder or overwrite a different installation.

A private repository requires an authorized GitHub account and valid local
authentication. Use existing local credentials; never embed a repository token
in an installation prompt or shared file.

Use a temporary download directory. Install only the two skill directories,
not a repository's historical or generated project files.

## 2. Python and dependencies

Use an available Python 3.10+ interpreter. If Codex provides a bundled working
Python, it may be used; otherwise ask for approval to install Python. Never copy
an absolute interpreter path from someone else's computer.

Resolve `<PPT_MASTER_DIR>` from the installed sibling engine and run:

```text
<PYTHON> -m pip install -r <PPT_MASTER_DIR>/requirements.txt
<PYTHON> -c "import pptx, fitz, mammoth, requests; from PIL import Image; print('Core imports OK')"
<PYTHON> <PPT_MASTER_DIR>/scripts/project_manager.py --help
<PYTHON> <PPT_MASTER_DIR>/scripts/svg_to_pptx.py --help
```

Run dependency installation and subsequent tools with the same interpreter.
On Windows, the interpreter may be `py -3`, `python`, or a resolved bundled
executable; on macOS/Linux it is commonly `python3`. Request network or file
permissions when required. Do not install optional system tools such as Pandoc
or Cairo until a task actually requires them.

## 3. Image relay configuration

AI images use the external hfsyapi service and require a user-provided key and
service balance. Read [`image-relay.md`](image-relay.md) when configuring or
using that service. No key is bundled in this repository.

For local configuration, copy `../relay.env.example` to `~/.ppt-master/.env`
only if that config does not already exist, then have the user enter the key
locally. Preserve existing configuration. Do not put a secret in prompts,
logs, committed files, manifests, or the installation report. Do not silently
replace the provider if a key is missing or the relay is unavailable.

## 4. Installation self-check

Confirm both `SKILL.md` files, the Wangyan design-library JSON, and the engine's
scripts/templates exist. Run the import and CLI checks above without calling
paid APIs. Check installed fonts against the selected design preset before
making a deck; use an available user-approved fallback when necessary.

Report the installed paths and the checks that actually ran. The skills should
be available on the next turn; restart Codex if discovery has not refreshed.

Use `$wangyan-ppt` as the presentation entry point. Keep source documents and
generated projects in the user's selected working folder.
