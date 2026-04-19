# Kingston Frameworks — Visual Identity

Ground truth for every video composition built in this workspace. Sourced from the Kingston Frameworks brand knowledge dump (April 2026). Every composition MUST trace its palette, typography, motion, and imagery choices back to this file.

**Company:** Kingston Frameworks — End-to-End Fine Art and Framing Solutions. Kingston & Belleville, Ontario. Archival custom framing since 1982. Platinum Award Winner 2025 (CommunityVotes Kingston, Picture Framing).

**Reference aesthetic:** [lowy1907.com](https://lowy1907.com). Quiet museum authority, craft-first imagery, heritage framing, minimal colour, understated typography. Goal: Lowy aesthetic + commercial UX.

**Owner:** Colin Morris. **Social (shared):** `@frameworkscanada` (Instagram, TikTok, Facebook).

## Style Prompt

Kingston Frameworks is a restrained, authoritative, craft-focused brand — "fine art studio, not framing shop." Compositions should feel like a private gallery at opening hour: warm near-black canvases, a single muted gold accent (never hot yellow), refined serif display type over clean body copy, documentary-workshop imagery, slow cinematic pacing. Not playful. Not hype. Not discount-driven. The mood is trust, preservation, longevity, quiet Canadian craft — a studio that has framed work for National Geographic, Queen's University, Cadillac Fairview, and The Tragically Hip, and talks about it as fact, not boast.

## Colors

| Token | Hex | Role |
|---|---|---|
| `--kf-bg` | `#0F0F0F` | Primary dark background |
| `--kf-bg-warm` | `#1A1612` | Warm near-black — preferred for large type, premium surfaces |
| `--kf-surface` | `#1A1A1A` | Cards, panels on dark |
| `--kf-surface-cream` | `#F8F6F0` | Warm light surface, editorial/gallery feel |
| `--kf-surface-white` | `#FFFFFF` | Pure white for modals, light-mode sections |
| `--kf-border` | `#2A2520` | Hairlines, dividers on dark |
| `--kf-gold` | `#B8960C` | Primary accent — muted pale gold, highlights only |
| `--kf-gold-glow` | `rgba(184,150,12,0.35)` | Subtle glow behind gold focal elements |
| `--kf-text` | `#FFFFFF` | Primary text on dark |
| `--kf-text-on-light` | `#1A1A1A` | Primary text on light surfaces |
| `--kf-text-dim` | `#6B7280` | Labels, metadata, captions |

**Three-colour discipline:** black + gold + white/cream. No fourth accent. If a secondary accent is ever needed, it must be confirmed with Colin before use — default is to solve the problem with restraint and contrast instead.

**Gold rule:** Pale, muted, premium. Never hot `#FFD700`. Gold is a highlight, never a large fill area. If more than ~5% of the frame is gold, reduce it.

**Black rule:** Prefer warm near-black (`#1A1612`) over pure black (`#000000`) for large surfaces and display type. Pure black reads harsh; warm black reads premium.

## Typography

- **Cormorant Garamond** — display serif. Use for: H1/H2, title cards, tagline reveals, generational-craft moments ("Since 1982"). Weights: 300 Light, 400 Regular, 600 SemiBold.
- **Montserrat** — sans body. Use for: body copy, lower-thirds, CTAs, labels, metadata. Weights: 400 Regular, 500 Medium, 600 SemiBold, 700 Bold.
- **JetBrains Mono** — monospace. Use for: prices, dimensions, DPI specs, technical metadata, archival ratings.

Pair Cormorant display over Montserrat body is the house pattern. Never use Cormorant for long body copy (illegible at small sizes). Never use more than two fonts in a single scene — adding a third dilutes brand recognition.

**Type scale (16px base):**

| Role | Size | Line-height | Weight | Case |
|---|---|---|---|---|
| H1 (display) | 48–56 px | 1.10 | Cormorant 600 | Title case |
| H2 | 36–40 px | 1.15 | Cormorant 600 or Montserrat 700 | Title case |
| H3 | 24–28 px | 1.20 | Montserrat 600 | Title case |
| Body | 16–18 px | 1.60 | Montserrat 400 | Sentence case |
| Caption / meta | 13–14 px | 1.40 | Montserrat 500, `letter-spacing: 0.02em` | Sentence case |
| Technical (prices, dimensions) | 14–16 px | 1.30 | JetBrains Mono 400, `font-variant-numeric: tabular-nums` | As-is |

**Grammar conventions:** Canadian English. Oxford comma. Title case for H1/H2 and ad headlines. Sentence case for body copy. No emoji in body copy; `📍` allowed only for location callouts in social ads.

## Logo

- **Status:** logo asset TBD. A placeholder file lives at `assets/Kingston_Logo.svg` (text wordmark in Cormorant Garamond + gold rule + tagline) until the canonical SVG from Colin/Dasha replaces it.
- Colin has stated the wordmark stays as-is — only surrounding colors and usage are being refined.
- **Clearspace (recommended):** padding equal to the cap-height of the wordmark on all sides.
- **Min size (recommended):** 24 px height on digital, 20 mm on print.
- Never recolor. Never stretch. Never add drop shadows, glows, or effects outside the approved gold-glow recipe (CSS: `filter: drop-shadow(0 0 24px rgba(184, 150, 12, 0.35));` — reserve for hero moments only).

## Motion Rules

Premium restraint. Never bouncy, never spring, never rotational. Every motion should feel like a gallery curtain pulling back, not a slot machine.

- **Easing palette:**
  - Primary: `cubic-bezier(0.32, 0.72, 0, 1)` (`--ease-refined`) — luxurious settle, use for all reveals and headline entrances.
  - Hover / micro: `cubic-bezier(0.4, 0, 0.2, 1)` (`--ease-hover`) — standard Material for quick interactions.
  - GSAP equivalents: `expo.out`, `power3.out`, `power4.out` for entrances; `power2.in` for hand-offs into transitions; `sine.inOut` for ambient loops.
- **Duration bands:** fast 150 ms, medium 300 ms, slow 600 ms, reveal 900 ms. Display type reveals can sit at 900–1200 ms.
- **Offset first animation** 0.15–0.30 s from scene start — let the canvas breathe before anything moves.
- **Text stagger:** 0.04–0.06 s per character for display type; 0.10–0.16 s per word for headlines.
- **Numbers / years:** use GSAP count-up with `{innerText: N, snap: {innerText: 1}}`, add `font-variant-numeric: tabular-nums` to avoid digit shuffle.
- **Entrance only** per the Hyperframes rule — `gsap.from()` everywhere; scene transitions handle exits.
- **Subtle hover / idle animations:** opacity drift 0.98–1.02, never rotation or scale-bounce.

## Transitions

Prefer CSS-driven transitions over shader blocks for premium restraint.

| Scene change | Transition | Duration | Ease |
|---|---|---|---|
| Opener → scene 2 | Slow cross-dissolve | 0.60 s | `sine.inOut` |
| Scene to scene (match) | Match-cut on beat | 0 s | n/a — hard cut on audio hit only |
| Scene to scene (time passage) | Cinematic cross-dissolve | 0.80 s | `sine.inOut` |
| Pre-reveal | Cinematic zoom (slow push-in) | 0.90 s | `expo.out` |
| Outro hand-off | Blur crossfade | 0.60 s | `sine.inOut` |
| Humour beat (sparingly) | Whip pan | 0.25 s | `expo.out` |

Avoid: glitch, VHS/RGB-split, light-leaks, SDF iris, rotation wipes, stock After Effects "handy seamless" packs.

## Buttons / CTAs

Rounded pill or clean rectangle, transparent fill, 1 px `--kf-gold` or `--kf-text-dim` border, Montserrat SemiBold 14–16 px, 12–16 px vertical + 24–32 px horizontal padding. Title case. No uppercase shouting.

Examples:
- `[ Book a consultation → ]`
- `[ Request a quote ]`
- `[ View the gallery ]`

Never: `[ FREE QUOTE!!! ]`, `[ SHOP NOW 🔥 ]`, `[ CLAIM YOUR DISCOUNT ]`.

## Iconography

Outlined, thin-stroke, minimalist. 1.5 px stroke on 24 px grid. 2 px corner radius — subtle softness, not fully rounded, not sharp. Gold (`--kf-gold`) or white (`--kf-text`) stroke on dark backgrounds; warm black (`--kf-bg-warm`) on light. No fills. Reference set: Lucide.

## Imagery Style

Photo-first. Real workshop, real installs, real frames on real walls. Avoid stock lifestyle shots and obvious AI artifacts.

**Three reference directions:**
1. **Installed work:** natural-light interior with tall ceilings, neutral walls (soft linen white), a single framed piece above a minimal oak console. Morning light, soft shadows, no people. Composition emphasizes the frame's shadow on the wall — the piece breathes.
2. **Workshop craft:** close-up, master framer's hands beveling a matboard on a wooden cutting surface. Warm tungsten light, brass tools visible, slight grain. Documentary, not staged.
3. **Gallery product:** single framed canvas on a deep charcoal wall, track-lit, slight vignette. No props, no lifestyle. The frame is the subject.

**Sources, in priority order:**
1. Original photography from Kingston Frameworks' Kingston and Belleville workshops and completed installs.
2. AI-generated via the NanoBanano Pro skills (`art-product-prompt-gen`, `interior-design-prompt-gen`) — only when the shot passes a "doesn't look AI at a glance" test.
3. Unsplash — fallback for generic environmental shots only.

**Never use:** staged "smiling woman holds frame" stock, bright saturated overlays, AI images with hand/proportion glitches, anything that reads as a big-box framing chain.

## Voice & Messaging

**Tone adjectives:** trusted, expert, restrained, authoritative, warm (local), discreet, Canadian, craft-focused, neighbourly, premium-but-not-flashy.

**Headline rule:** every claim attributed to a concrete fact. "Since 1982," "Platinum Award 2025," "64-inch wide-format printing," "Hahnemühle archival papers." Never "best," "unbeatable," "#1 choice."

**Headline examples (in use):**
- "End-to-End Fine Art and Framing Solutions"
- "Archival custom framing since 1982"
- "Your art deserves a frame as exceptional as the work itself"
- "Museum-grade framing"
- "Book a free design consultation"

**Word palette — YES:** archival · conservation · museum-grade · handcrafted · end-to-end · full-cycle · since 1982 · locally handcrafted · certified · fine art · craftsmanship · discreet · expert · preservation · reversible mounting.

**Word palette — NO:** cheap · affordable · best in Canada · amazing · awesome · incredible · limited time only · hurry · FREE!!! · game-changer · revolutionary · unbeatable prices · #1 choice · simply the best · mom-and-pop shop.

## What NOT to Do

1. **No hot yellow gold.** Only muted pale gold `#B8960C`. Hot `#FFD700` reads cheap.
2. **No pure black `#000` for large surfaces.** Use warm `#1A1612` for display type and premium backgrounds.
3. **No emoji in body copy.** `📍` allowed only for location callouts in social ads.
4. **No casual celebrity/client name-dropping.** Use logos or quantified-outcome framing, always with discretion.
5. **No countdown timers, "FREE!!!," or discount shouting.** Premium positioning leads with craft and outcome, price revealed at commitment moment.
6. **No cartoon illustrations, hand-drawn styles, or playful characters.** Imagery is photographic or minimal geometric only.
7. **No "framing shop."** Always "studio," "fine art studio," or "Frameworks."
8. **No more than two fonts per scene.** Cormorant + Montserrat (or Montserrat + JetBrains Mono). Never a third.
9. **No hype music, EDM drops, or whoosh SFX.** Minimal neo-classical / ambient cinematic, 60–90 BPM, instrumental only, subtle crescendo at reveal.
10. **No glitch / VHS / RGB-split / light-leak / rotation-wipe transitions.** Clean cuts on beat, match cuts, slow cross-dissolves, cinematic zooms only.
11. **No spinning logos, particle explosions, or spring-bounce animations.** Luxurious settle only.
12. **No stretching the logo.** Keep aspect ratio. Respect clearspace.
13. **No `Math.random()` or `Date.now()`** — render determinism. Use seeded PRNG if needed.
14. **No exit animations** on any scene except the final one — transitions handle exits.

## File References

- `assets/brand-tokens.css` — the CSS `:root` custom props imported by every composition
- `assets/Kingston_Logo.svg` — placeholder wordmark (TODO: replace with canonical SVG from Colin/Dasha)
- `assets/_legacy-ais/` — archived AIS worked-example (reference only, do not use for Kingston production)

## Gaps & Open Questions

The following remain unresolved and should be confirmed with Colin/Dasha before production use:

1. **Canonical logo SVG** — current asset is a placeholder.
2. **Exact gold shade** — `#B8960C` is the anchor from the KingFrame build plan; Colin wanted to experiment with ochre variants. Alternatives on the table: `#C9A961` (lighter ochre), `#9A7B0A` (darker premium).
3. **Legal entity name** — operating names are `Kingston Frameworks`, `Frameworks Canada`, `Belleville Frameworks`. Legal entity not confirmed.
4. **Trademark status** — CIPO registry not yet checked.
5. **Public contact email + phone** — not yet documented for video CTA use.
6. **Street addresses** — Kingston and Belleville locations not in this file; pull from site when needed.
7. **Music library accounts** — Artlist / Musicbed / Epidemic credentials and canonical track whitelist TBD.
