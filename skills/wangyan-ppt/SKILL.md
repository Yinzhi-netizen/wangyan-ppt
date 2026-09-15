---
name: wangyan-ppt
description: >
  Create or redesign polished 16:9 presentations with the existing PPT Master
  SVG-to-PPTX pipeline, using Wangyan's curated visual design library and the
  hfsyapi.cn OpenAI-compatible image relay by default. Use for "生成PPT",
  "做演示文稿", "重新设计PPT", or when the user asks for Wangyan PPT style.
---

# Wangyan PPT Skill

Use this as the preferred presentation entry point. The existing `ppt-master`
directory remains the execution engine; this skill adds the Wangyan style
decision layer and a repeatable image-relay path.

## Installation and portable paths

Install this skill and `ppt-master` into the same parent skills directory.
Resolve `WANGYAN_DIR` from this file's actual location and `PPT_MASTER_DIR` as
its sibling `../ppt-master`; do not assume a particular username, drive, clone
directory, or current working directory. Run engine scripts by their resolved
absolute paths. Keep generated projects in the user's chosen workspace, not
inside either installed skill directory.

If the sibling engine or Python dependencies are missing, follow
[`references/install.md`](references/install.md). Do not overwrite an existing
skill installation without approval. The design workflow below is unchanged.

## 1. Load the engine and the Wangyan library

Read these files before changing or generating a deck:

1. `../ppt-master/SKILL.md` — authoritative serial pipeline, gates, SVG rules,
   export commands, and role references.
2. `references/design-library.md` — visual presets and selection rules.
3. `references/design-library.json` — machine-readable palette and typography
   values when writing `design_spec.md` or `spec_lock.md`.

Do not duplicate or replace the engine workflow. Follow its source conversion,
project initialization, Eight Confirmations, sequential SVG authoring, quality
check, post-processing, and export gates.

## 2. Wangyan design decision layer

Apply precedence in this order:

| Priority | Source | Action |
|---|---|---|
| 1 | Explicit user style, colors, template path, or reference deck | Preserve the request exactly where technically compatible. |
| 2 | A supplied Wangyan reference deck or an existing project style | Extract its visual logic and map it to the closest library preset. |
| 3 | `references/design-library.md` | Select one preset from audience, subject, mood, and light/dark needs. |
| 4 | Legacy PPT Master defaults | Use only when the library has no suitable match. |

Lock one base preset per deck. Do not mix unrelated presets on adjacent pages.
Small content-driven variations are allowed only as page-level rhythm changes;
the background, primary, body text, border, font stack, and icon library stay
deck-wide and are written to `spec_lock.md`.

The default Wangyan output is concise, high-end, and presentation-readable:
16:9 canvas, generous negative space, one dominant idea per page, asymmetric
editorial grids, restrained accents, native SVG text and charts, no nested card
stacks, and border radius no greater than 6px. Preserve source wording and
slide order when redesigning an existing deck.

## 3. Image acquisition: hfsyapi relay first

When the Strategist creates any `Acquire Via: ai` row, use the procedure in
[`references/image-relay.md`](references/image-relay.md). The default provider
is the OpenAI-compatible hfsyapi.cn relay, not a different provider chosen by
habit. Keep all editable titles, body copy, data, labels, logos, and citations
in SVG; generated images contain no such text.

Required execution shape:

```text
Strategist writes image_prompts.json
  -> validate UTF-8 without BOM and required fields
  -> run the manifest through hfsyapi relay
  -> inspect Generated / Failed / Needs-Manual statuses
  -> verify dimensions and filenames
  -> Executor embeds only verified images
```

Use `image_gen.py --manifest` for the normal path, after the IPv4-first check in
[`references/image-relay.md`](references/image-relay.md). If the configured
relay backend is unavailable, or the Windows request path hits a dual-stack
timeout/`WinError 10013`, follow the documented direct OpenAI-compatible
request fallback with `curl.exe -4`; never silently switch providers and never
print or commit secrets.

## 4. Motion discipline: restrained by default

Wangyan decks are calm and editorial; motion must match. The engine's export
default (`-a auto` + `after-previous`) animates **every** top-level `<g id>`
group — on dense lecture pages that reads as "every text box flying in". This
is the single most common complaint. Apply these rules on every deck:

**Executor grouping = animation granularity.** One `<g>` per content block
(a whole list column, a whole card row), never one per bullet/line. If a page
has more than ~8 non-chrome top-level groups, the grouping is too fine —
merge before worrying about animation flags.

**Default export for Wangyan decks** — write `animations.json` at export time
that fades in at most 1–2 groups per page and sets every other content group
to `"effect": "none"`:

| Animate (fade, order 1-2) | Set `none` |
|---|---|
| Hero visual (`figure-*`, `hub`, `timeline-track`, `cycle-ring`, `pyramid`, `cover-title`, `chapter-block`, `break-block`, `big-question`) | all other content groups (list items, chips, table rows, labels) |
| The page's takeaway (`key-idea`, `key-question`, `quote-block`, `statement`, `formula-strip`, `takeaway`) | |

Generate the sidecar by scanning `svg_output/*.svg` for top-level `<g id>`,
whitelisting the patterns above, marking everything else `none`, then
`animation_config.py validate <project>` before export. Unlisted groups still
get the default animation — silencing must be explicit. Page transitions stay
at the `fade` default.

Only animate more when the user explicitly asks (then run the
`customize-animations` workflow).

## 5. Platform notes learned from real runs

- **Windows QA rendering**: when LibreOffice is absent, export slide PNGs via
  PowerPoint COM (`$pres.Export($dir,'PNG',1280,720)`) for the visual QA loop.
- **Font stacks**: write multi-word families unquoted in `spec_lock.md` and
  SVG `font-family` (`Arial, Microsoft YaHei, sans-serif`, not
  `Arial, "Microsoft YaHei", sans-serif`). Both parse identically downstream,
  but quoted forms break `svg_quality_checker.py`'s spec-drift matching
  (its regex stops at the first inner quote) and produce false drift warnings.
- **gpt-image-2 via hfsyapi** supports `21:9` — use it for top-band case-study
  images instead of cropping 16:9.

## 6. Handoff requirements

Before reporting completion, verify:

- `design_spec.md` records the selected Wangyan preset and its rationale.
- `spec_lock.md` contains the final colors, fonts, icon library, page rhythm,
  and image paths used by every SVG page.
- Every AI image row is resolved or explicitly marked `Needs-Manual` with the
  error preserved.
- Motion follows §4: `animations.json` exists, animates at most 1–2 groups per
  page, and passed `animation_config.py validate`.
- SVG quality checks pass, the PPTX export exists, and the exported deck is
  opened or rendered for visual inspection.

Never claim final delivery from a valid ZIP/PPTX alone; content and visual QA
are part of completion.
