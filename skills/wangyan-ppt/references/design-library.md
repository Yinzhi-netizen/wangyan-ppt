# Wangyan Design Library

Curated visual presets distilled from the family's accepted presentation work.
Use one preset as the deck-wide identity, then adapt page rhythm to content.

**Version**: 1.2.0 | **Last Updated**: 2026-09-01

## 1. Selection rules

| Signal | Preset |
|---|---|
| Academic, policy, strategy, lecture; calm premium editorial | `wangyan-light-editorial` |
| Conference argument, manifesto, provocative thesis, dark stage | `wangyan-dark-editorial` (⚠️ not recommended for general use) |
| Chinese executive briefing, finance, technology transfer, management | `wangyan-executive-briefing` |
| Asia-Pacific policy, technology cooperation, innovation ecosystem | `wangyan-apec-technology` |
| Environmental policy, ESG, sustainable development, green transformation | `wangyan-sustainable-strategy` |
| Policy research, think tank, academic institution, historical analysis | `wangyan-classic-institute` |

If two signals conflict, prefer the user's explicit mood, then audience. For a
reference deck, preserve its light/dark behavior and map colors to the closest
preset rather than copying isolated colors without their contrast relationships.

## 2. Presets

### 2.1 `wangyan-light-editorial`

**Character**: top-consulting clarity with Swiss editorial restraint; warm ivory
field, deep pine structure, cinnabar emphasis, dark chapter anchors.

**Palette**:

| Role | HEX |
|---|---|
| Background | `#F4F1EA` |
| Secondary background | `#E6E1D7` |
| Primary | `#173E38` |
| Accent | `#D55A3D` |
| Secondary accent | `#8DA69A` |
| Body text | `#1D2321` |
| Secondary text | `#5E6863` |
| Border | `#C9C3B8` |

**Typography**: titles `Georgia, "Microsoft YaHei", serif`; body
`Arial, "Microsoft YaHei", sans-serif`; body 22px, title 40px, cover 72px,
chapter 56px, annotation 15px.

**Layout**: full-bleed cover/chapter atmosphere; breathing pages with one
claim; dense pages with asymmetric split, three-column comparison, timeline, or
center-radiating framework. Use 60px safe margins and 28–36px block gaps.

### 2.2 `wangyan-dark-editorial`

**Character**: black-paper academic editorial; warm ivory type, vermilion
argument markers, quiet sage support, strong negative space for projection.

**Palette**:

| Role | HEX |
|---|---|
| Background | `#000000` |
| Secondary background | `#121212` |
| Primary | `#F5F1E8` |
| Accent | `#FF6A4A` |
| Secondary accent | `#A7B1AB` |
| Body text | `#E4E0D7` |
| Secondary text | `#A7B1AB` |
| Border | `#343434` |

**Typography**: titles `Georgia, "Microsoft YaHei", serif`; body
`Arial, "Microsoft YaHei", sans-serif`; body 22px, title 40px, cover 72px,
chapter 56px, hero question 180px.

**Layout**: anchor pages use full-bleed atmospheric images and sparse text;
thesis pages are breathing pages; evidence pages use thin rules and one
dominant native diagram. Keep accent under roughly 10% of visible area.

### 2.3 `wangyan-executive-briefing`

**Character**: CJK-first executive technology briefing; warm-white content
pages, graphite navy hierarchy, restrained Chinese red, analytical teal.

**Palette**:

| Role | HEX |
|---|---|
| Background | `#F6F3EE` |
| Secondary background | `#E9EDF0` |
| Primary | `#102A43` |
| Accent | `#B43B34` |
| Secondary accent | `#287A8B` |
| Body text | `#18212B` |
| Secondary text | `#52606D` |
| Border | `#C8D0D7` |

**Typography**: all primary roles `"Microsoft YaHei", Arial, sans-serif`;
body 18px, title 32px, cover 54px, chapter 44px, annotation 14px.

**Layout**: 12-column grid, thin header rule, flat figure panels, dark-anchor
chapter pages, and restrained source cues in the footer. Existing charts,
screenshots, labels, and data remain intact when redesigning.

### 2.4 `wangyan-apec-technology`

**Character**: premium editorial technology illustration for policy and
innovation ecosystems; deep navy base, cool blue networks, small warm-gold
glints, calm overlay regions.

**Palette**:

| Role | HEX |
|---|---|
| Background | `#F7F8FA` |
| Secondary background | `#FFFFFF` |
| Primary | `#12324A` |
| Deep anchor | `#0B1F33` |
| Accent | `#2F80ED` |
| Secondary accent | `#C8A45D` |
| Body text | `#20242A` |
| Secondary text | `#667085` |
| Border | `#D9DEE7` |

**Typography**: `DengXian, "Microsoft YaHei UI", "Microsoft YaHei", Arial,
sans-serif`; body 18px, title 34px, cover 60px, chapter 44px.

**Layout**: technology and policy maps, hub-and-spoke diagrams, pyramids,
matrices, and numbered process pages. Use blue for analytical emphasis and
gold only for small highlights; keep the center calm when an image receives
native SVG overlays.

### 2.5 `wangyan-sustainable-strategy`

**Character**: restrained strategic reporting for environmental and sustainability
topics; warm-neutral canvas, deep strategic green, ancient copper accent, cool
grey for comparison.

**Palette**:

| Role | HEX |
|---|---|
| Background | `#F7F8F5` |
| Secondary background | `#ECEEED` |
| Primary | `#173B2F` |
| Accent | `#B9824A` |
| Secondary accent | `#485E6F` |
| Body text | `#20242A` |
| Secondary text | `#5D656B` |
| Border | `#D6DAD5` |

**Typography**: `"Microsoft YaHei", Arial, sans-serif` for all roles;
body 20px, title 34px, cover 50px, chapter 44px.

**Layout**: strategic green as anchor rather than decoration; copper gold used
sparingly for key emphasis only. Documentary image style with calm regions for
overlay. Hub-spoke networks, layered systems, timeline progressions.

### 2.6 `wangyan-classic-institute`

**Character**: authoritative policy/think-tank reporting with new-Chinese
editorial restraint; ivory canvas, deep ink-blue structure, ancient copper-gold
emphasis, academic weight.

**Palette**:

| Role | HEX |
|---|---|
| Background | `#F7F5F0` |
| Secondary background | `#EFEBE2` |
| Primary | `#1B2A4A` |
| Accent | `#B08D57` |
| Secondary accent | `#5B7290` |
| Body text | `#1D1D1F` |
| Secondary text | `#4A5568` |
| Border | `#D8D0C0` |

**Typography**: `"Microsoft YaHei", Arial, sans-serif` for all roles;
body 18px, title 32px, cover 54px, chapter 44px.

**Layout**: thin header rules, flat information panels, ink-blue chapter anchors,
restrained source citations in footer. Existing charts and data remain intact.
Classic editorial grids with breathing asymmetry.

## 3. Shared Wangyan composition rules

| Rule | Requirement |
|---|---|
| Hierarchy | One dominant claim, one supporting visual structure. |
| Rhythm | Alternate `anchor`, `dense`, and `breathing` pages; avoid an all-card deck. |
| Text | Preserve supplied wording; keep long copy out of generated images. |
| Color | Use background 55–75%, primary 15–30%, accent usually under 10%. |
| Geometry | 16:9 `1280x720`; safe margins 60–72px; radius <= 6px. |
| Icons | Use one library only, normally `tabler-outline`, 2px stroke. |
| Images | Prefer documentary or abstract editorial composition with deliberate calm regions. |
| Motion | Restrained: fade transitions; at most 1–2 entrance groups per page (hero + takeaway) via `animations.json`; never per-bullet animation. |
| Forbidden | Random palettes, mixed icon libraries, decorative gradients in native SVG, nested card stacks, tiny body text, or invented data. |

## 4. Recording the decision

In `design_spec.md`, name the preset in `III. Visual Theme` and explain any
user-requested deviations. In `spec_lock.md`, write the resolved HEX values,
font stacks, icon library, `image_rendering`, and `image_palette`; every SVG
page must read these locked values before authoring.
