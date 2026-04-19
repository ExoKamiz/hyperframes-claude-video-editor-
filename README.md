# Kingston Frameworks — Video Production Workspace

A motion-graphics pipeline for **Kingston Frameworks** built on **plain HTML + GSAP** via [Hyperframes](https://hyperframes.heygen.com). One repo, one set of brand tokens, one growing library of video work.

> This is **not** a Remotion / React / Next.js stack. Every composition here is a regular HTML file with a paused GSAP timeline attached to `window.__timelines`. The Hyperframes CLI handles lint, preview, and render.

**Owner:** Colin Morris. **Brand:** Kingston Frameworks, end-to-end fine art and framing solutions, Kingston & Belleville, Ontario, since 1982.

---

## Prerequisites

- **Node 20+** — run `node --version` to check
- **FFmpeg** on your `PATH` — needed for audio extraction and re-encoding
- **Chrome (latest)** — Hyperframes renders through a headless Chromium
- **~5 GB free disk** — node_modules is chunky; renders are bigger
- **16 GB RAM recommended** for smooth Studio preview with multiple shader blocks

Run `npx hyperframes doctor` after `npm install` — it reports what's missing.

## Quickstart

```bash
git clone <repo-url> kingston-frameworks-video
cd kingston-frameworks-video
npm install

# Optional — only if you want ClickUp / OpenAI integrations
cp .env.example .env
# ...then edit .env with your own keys

# Open Studio on a project
cd video-projects/claude-edit-intro
npx hyperframes preview    # http://localhost:3002
```

Studio hot-reloads on file save. Scrub the timeline, inspect scenes, change colors, watch it re-render live.

## Repo layout

```
kingston-frameworks-video/
├── README.md                    ← you are here
├── LICENSE                      ← MIT (see note on brand assets)
├── .env.example                 ← copy to .env, fill in your own keys
├── CLAUDE.md                    ← workspace guide for Claude Code users
├── AGENTS.md                    ← agent-delegation notes
├── MOTION_PHILOSOPHY.md         ← the motion aesthetic this workspace aspires to
├── DESIGN.kingston.md           ← Kingston Frameworks visual identity (canonical)
├── assets/                      ← shared Kingston brand assets
│   ├── brand-tokens.css         ← Kingston CSS custom props (--kf-*)
│   ├── Kingston_Logo.svg        ← placeholder wordmark (TODO: canonical SVG)
│   └── _legacy-ais/             ← archived AIS worked-example (reference only)
├── docs/                        ← longer-form specs + plans
├── scripts/                     ← workspace-level preflight scripts
├── .claude/                     ← Claude Code skills (drop-in slash commands)
│   ├── launch.json
│   └── skills/                  ← /hyperframes, /gsap, /make-a-video, etc.
├── package.json
└── video-projects/              ← video projects, one folder each
    └── <project>/
        ├── index.html           ← root composition entry
        ├── compositions/        ← sub-comps loaded via data-composition-src
        ├── assets/              ← video, audio, images, transcripts
        ├── final.mp4            ← the target output
        ├── renders/             ← local render scratch (gitignored)
        ├── hyperframes.json     ← CLI config (paths relative to this folder)
        ├── meta.json            ← id / name / dimensions / fps
        └── (STORYBOARD.md, HANDOFF.md, NOTES.md as applicable)
```

## Video projects

This workspace hosts two generations of video work.

### Kingston Frameworks production (active)

Use these as starting templates for new Kingston video work. Each imports `assets/brand-tokens.css` and follows `DESIGN.kingston.md`.

| Project | What it is |
|---|---|
| `claude-edit-intro` | Promo-style intro to an editing workflow; minimal brand hardcoding — easiest starting template. |
| `clickup-demo` | 60s SaaS product demo — heavy registry-block use (x-post, ui-3d-reveal). Five render versions show the iteration curve. |
| `first-agent-promo` | 32s launch film. Uses a React-via-Babel approach instead of the standard HTML pattern — a useful counter-example. |
| `hyperframes-sizzle` | Hyperframes × Claude Code sizzle reel. Uses the `/website-to-hyperframes` flow. |
| `linear-promo-30s` | 30s Linear-style promo in the Infinite Payments aesthetic. Ships as a draft — good exercise ground. See `NOTES.md`. |
| `may-shorts-6` | Landscape 16:9 cut of a talking-head short. |
| `may-shorts-18` | Earlier vertical short; compare against `may-shorts-19` to see what got refined. |
| `may-shorts-19` | Most polished short-form vertical in the workspace. The `/short-form-video` skill was written around it. |

### Legacy archive (AIS worked-example)

These projects were built under the original AIS (AI Automation Society) brand and are retained as reference only. Each has a `LEGACY.md` explaining what not to inherit. **Do not use AIS tokens, hex values, or copy in Kingston production.**

| Project | Why it's here |
|---|---|
| `aisoc-hype` | 30s AIS brand hype film — scaffold many other AIS projects reference. |
| `aisoc-app-release` | 30s AIS mobile app release promo. `HANDOFF.md` documents the original footguns. |
| `aisoc-lesson-5-1` | Full lesson video (face-cam + motion graphics). |
| `golden-ratio-demo` | AIS lesson on proportion in layout. Ships as a polished draft. |

## Brand system

Kingston Frameworks is built on a restrained three-colour palette and two-font pairing. See `DESIGN.kingston.md` for the full spec.

| Token | Hex | Role |
|---|---|---|
| `--kf-bg` | `#0F0F0F` | Primary dark background |
| `--kf-bg-warm` | `#1A1612` | Warm near-black for display type / premium surfaces |
| `--kf-surface-cream` | `#F8F6F0` | Warm light surface |
| `--kf-gold` | `#B8960C` | Muted pale gold — highlights only, never hot yellow |
| `--kf-text` | `#FFFFFF` | Primary text on dark |
| `--kf-text-dim` | `#6B7280` | Labels, metadata |

**Typography:** Cormorant Garamond (display serif) + Montserrat (body sans) + JetBrains Mono (technical / prices). Never more than two fonts in a single scene.

**Reference aesthetic:** [lowy1907.com](https://lowy1907.com) — quiet museum authority, craft-first imagery, heritage framing, minimal colour.

### Find-and-fix sweep

If you suspect stale AIS tokens or hardcoded hex values have leaked into a Kingston composition, run:

```bash
# Finds any legacy AIS tokens or hex values in active projects
grep -rEn "(--ais-|#37bdf8|#f09025|#07121c|#195066|#0d2031|aisoc|AIS Logo|@aiautomationsociety)" \
  video-projects/ \
  --exclude-dir=aisoc-hype \
  --exclude-dir=aisoc-app-release \
  --exclude-dir=aisoc-lesson-5-1 \
  --exclude-dir=golden-ratio-demo
```

Any hit in an active Kingston project should be replaced with the matching `--kf-*` token from `assets/brand-tokens.css` or the Kingston hex values above.

## Creating a new Kingston video project

1. Pick a kebab-case name: `mkdir video-projects/kingston-workshop-tour`
2. Scaffold with the CLI or copy a sibling:
   ```bash
   cd video-projects/kingston-workshop-tour
   npx hyperframes init
   ```
   Or, faster: copy the `hyperframes.json` + `meta.json` from an active project (e.g. `claude-edit-intro`), edit `meta.json` for the new id/name/dimensions, and start on `index.html` from scratch.
3. Install the shared brand assets:
   ```bash
   cp ../../assets/brand-tokens.css assets/
   cp ../../assets/Kingston_Logo.svg assets/
   ```
4. Read `DESIGN.kingston.md` before any visual decision. It's the canonical brand spec.
5. Build. Preview. Lint. Render.

## The authoring loop

```
edit → lint → preview (Studio, live) → draft render → verify frames → final render
```

| Step | Command | What to check |
|---|---|---|
| Lint | `npx hyperframes lint` | Zero errors before you preview. Warnings are survivable. |
| Preview | `npx hyperframes preview` | Scrub the timeline, fix anything weird live. Hot reload works. |
| Draft render | `npx hyperframes render --quality draft --output renders/draft.mp4` | ~1–3 minutes. CRF 28 — pixelated but fast. |
| Verify frames | `ffmpeg -ss <t> -i renders/draft.mp4 -frames:v 1 out.png` | Pull one frame per scene at its hero moment. Look for cropped faces, misaligned text, blank frames. |
| Final render | `npx hyperframes render --quality standard --output renders/final.mp4` | Visually lossless 1080p. Ship this. |

> **`MOTION_PHILOSOPHY.md` is the aesthetic baseline.** Before you build anything, read section 0 (the 10 Laws) and section 4 (pre-flight checklist). It's the difference between "it rendered" and "it's good."
>
> **`DESIGN.kingston.md` is the brand contract.** Every colour, font, and motion choice must trace back to it.

## Recommended reading order

1. **This README** (you're here)
2. **`CLAUDE.md`** — full workspace guide, conventions, skills, render contract. The 11 Render Contract rules apply to anyone editing a composition.
3. **`MOTION_PHILOSOPHY.md`** — aesthetic rules. Read before brainstorming.
4. **`DESIGN.kingston.md`** — Kingston visual identity.
5. **Open `claude-edit-intro`** — minimal brand hardcoding, easy to read. `index.html` + `final.mp4` side by side, then the `compositions/` folder.

## Using Claude Code with this repo

The `.claude/skills/` folder ships slash commands that encode framework-specific patterns (`window.__timelines` registration, `data-*` attribute semantics, shader-compatible CSS). If you use [Claude Code](https://claude.com/claude-code), these unlock automatically:

- `/hyperframes` — authoring/editing compositions, captions, TTS, audio-reactive animation
- `/hyperframes-cli` — CLI reference (init, add, lint, preview, render, transcribe, tts)
- `/gsap` — GSAP animation: timelines, easing, stagger, plugins
- `/hyperframes-registry` — install catalog blocks/components
- `/website-to-hyperframes` — turn a URL into a composition (7-step capture-to-video)
- `/make-a-video` — end-to-end beginner flow
- `/short-form-video` — 9:16 talking-head + motion graphics playbook

Not a Claude Code user? The skills are just markdown — open them up and read as documentation.

## Troubleshooting

| Symptom | First thing to try |
|---|---|
| `npx hyperframes` — command not found | `npm install` in the repo root first |
| Render fails mid-way | `npx hyperframes doctor` — verifies Node, FFmpeg, Chrome |
| Studio preview stuck at 0s | Hard-refresh (Ctrl+Shift+R). If that fails, try a specific sub-composition URL: `http://localhost:3002/?comp=<sub-comp-id>` |
| Lint errors about overlapping clips | Two clips on the same `data-track-index` overlap in time — assign different indices or adjust `data-start` / `data-duration` |
| Lint errors about `missing_gsap_script` | Every sub-composition HTML needs its own `<script src="https://cdn.jsdelivr.net/npm/gsap@3.14.2/dist/gsap.min.js"></script>` before its IIFE — GSAP doesn't inherit from the parent |
| Video frozen in a render, audio continues | A `<video>` element was animated directly (don't animate `width`/`height`/`top`/`left` on a `<video>`). Wrap it in a `<div>` and animate the wrapper. |

More: `npx hyperframes docs <topic>` (topics: `data-attributes`, `gsap`, `rendering`, `examples`, `troubleshooting`, `compositions`).

## Credits and license

- **Code and compositions** — MIT, see `LICENSE`.
- **Kingston Frameworks brand assets** (logo, brand tokens, DESIGN.kingston.md) — © Kingston Frameworks. Not licensed for reuse outside Kingston Frameworks production.
- **Legacy AIS brand assets** (`assets/_legacy-ais/`) — remain the property of AI Automation Society, retained for archival reference only; not licensed for reuse.
- **Hyperframes** — framework © HeyGen, docs at https://hyperframes.heygen.com.
