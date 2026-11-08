# Daybook Design System
**Bizzie Media Group / Stephanie Elie** — brand visual system for web, social, and product surfaces.

This file is the canonical reference for Daybook. Use it as a project-root `DESIGN.md` for any tool that reads repo-level design context (Claude Code, Cursor, Windsurf, Copilot, v0, Bolt, Lovable, etc.).

---

## Brand Character

Daybook should read as warm, editorial, and slightly analog — like a creative studio's production log, not a polished corporate tech brand. It supports Stephanie Elie's personal brand and Bizzie Media Group's studio identity across Instagram, Reels, decks, and web.

Show assets (e.g. Alpha 8 cover art) are **studio-framed, never reskinned** — present them within the Daybook system (framed, captioned, contextualized), never apply Daybook colors/type directly on top of a show's own key art.

---

## Color Palette

### CSS Custom Properties

```css
:root {
  /* Surfaces */
  --color-canvas: #EDE8DC;   /* Stone — base background */
  --color-surface: #F8F4EA;  /* Paper — elevated surfaces / cards */

  /* Text */
  --color-text-primary: #221D18;   /* Graphite */
  --color-text-secondary: #6B6053; /* Slate */

  /* Structure */
  --color-border: #D8D0BF; /* Hairline */

  /* Accents */
  --color-accent-primary: #E8912B; /* Signal amber — primary CTA / emphasis */
  --color-accent-light: #F5B04D;   /* Marker — secondary emphasis / hover */
  --color-accent-cool: #1F4B47;    /* Circuit teal — sparing cool counterpoint */
}
```

| Token | Name | Hex | Role |
|---|---|---|---|
| `--color-canvas` | Stone | `#EDE8DC` | Default page/app background |
| `--color-surface` | Paper | `#F8F4EA` | Cards, panels, anything elevated above canvas |
| `--color-text-primary` | Graphite | `#221D18` | Primary text — no pure black anywhere |
| `--color-text-secondary` | Slate | `#6B6053` | Secondary/muted text |
| `--color-border` | Hairline | `#D8D0BF` | Dividers, borders, subtle separation |
| `--color-accent-primary` | Signal amber | `#E8912B` | Primary CTA, links, key emphasis |
| `--color-accent-light` | Marker | `#F5B04D` | Hover states, secondary emphasis |
| `--color-accent-cool` | Circuit teal | `#1F4B47` | Sparing cool contrast — not a primary color |

**Rules:**
- Never use pure black (`#000`) or pure white (`#FFF`) for text or backgrounds — always route through the tokens above.
- Circuit teal is a counterpoint, not a workhorse — avoid using it for large fills or default states.

---

## Typography

Daybook runs **three category stacks** over four shared roles — title, subtitle, body, handwriting. Pick the category by what the surface is for, then use the role tokens; never mix families across categories in one composition.

| Category | Use it for |
|---|---|
| **Creative** (default) | Bizzie Media Group studio surfaces, show-adjacent material, production-log content, decks |
| **Tech** | Content-systems and AI-governance work — portfolio, product UI, documentation, specs |
| **Lifestyle** | @bizzieliving — second-act brand, personal editorial, lifestyle social |

**Handwriting is Caveat in all three categories.** One handwritten voice across the whole system, by design — it is the only family that never changes with the category.

### CSS Custom Properties

Creative is the `:root` default. Set `data-daybook="tech"` or `data-daybook="lifestyle"` on `<html>` or any container to switch.

```css
:root {
  /* Creative — default */
  --font-title:    "Fraunces", Georgia, serif;
  --font-subtitle: "Bricolage Grotesque", system-ui, sans-serif;
  --font-body:     "DM Sans", system-ui, sans-serif;
  --font-hand:     "Caveat", cursive;
  --font-utility:  "Space Mono", monospace; /* constant — see Take Stamp */
}

[data-daybook="tech"] {
  --font-title:    "Space Grotesk", system-ui, sans-serif;
  --font-subtitle: "IBM Plex Mono", monospace;
  --font-body:     "IBM Plex Sans", system-ui, sans-serif;
}

[data-daybook="lifestyle"] {
  --font-title:    "Instrument Serif", Georgia, serif;
  --font-subtitle: "Manrope", system-ui, sans-serif;
  --font-body:     "Manrope", system-ui, sans-serif;
}
```

### Role Table

| Role | Creative | Tech | Lifestyle |
|---|---|---|---|
| Title | Fraunces | Space Grotesk | Instrument Serif |
| Subtitle | Bricolage Grotesque | IBM Plex Mono | Manrope |
| Body | DM Sans | IBM Plex Sans | Manrope |
| Handwriting | Caveat | Caveat | Caveat |

### Per-Family Specs

Weight ranges and italic availability below are confirmed against Google Fonts' published family metadata (checked 2026-11-07).

| Font | Weights | Italic | Notes |
|---|---|---|---|
| Fraunces | Variable 100–900 | **Yes** (real) | Also has `SOFT` (0–100) and `WONK` (0–1) axes — these carry most of its character. See axis note below. |
| Bricolage Grotesque | Variable 200–800 | **No** | Never fake-italicize. Also has `wdth` and `opsz` axes. |
| DM Sans | Variable 100–1000 | **Yes** (real) | Use italic for in-body emphasis. Has `opsz` (9–40). |
| Space Grotesk | Variable 300–700 | **No** | Never fake-italicize. Emphasis via weight, not slant. |
| IBM Plex Mono | Static 100–700 | **Yes** (real) | As a *subtitle* face in Tech — not the utility face. |
| IBM Plex Sans | Variable 100–700 | **Yes** (real) | Has `wdth` (75–100). |
| Instrument Serif | **400 only** | **Yes** (real) | ⚠️ Single weight — there is no bold. See constraint below. |
| Caveat | Variable 400–700 | **No** | 400 is the lightest available. Never fake-italicize. |

**Instrument Serif constraint (Lifestyle titles):** the family ships one weight, 400. There is no bold or semibold. Lifestyle titles must get their presence from **size** (scale up hard — 48px+ on web, large on social) rather than weight, and a bold Lifestyle headline is not available. Never let a tool synthesize bold from it — faux-bold on a 400-only serif smears the thin strokes. If Lifestyle needs a genuinely heavy headline, promote Manrope at 700–800 for that one piece and note the exception.

**Fraunces axis note (Creative titles):** Fraunces changes character substantially with `SOFT` and `WONK`. Daybook's warm/analog read wants some of both, not the flat default:

```css
.daybook-title--creative {
  font-family: var(--font-title);
  font-variation-settings: "SOFT" 40, "WONK" 1;
}
```

I have not verified in-browser that Google's served Fraunces file exposes `SOFT`/`WONK` when loaded via a weight-range request — confirm the axes actually respond before relying on them, and if they don't, pin them from Google Fonts' own embed panel instead.

### Subtitle vs. Body in Lifestyle

Lifestyle uses Manrope for both roles, so the two cannot differentiate by family. Separate them by weight and tracking:

```css
[data-daybook="lifestyle"] .subtitle {
  font-weight: 700;
  letter-spacing: -0.01em;
}
[data-daybook="lifestyle"] .body {
  font-weight: 400;
  letter-spacing: 0;
}
```

### Handwriting (Caveat) — Usage Rules

Caveat is an **accent voice, not a text face**. It carries the production-log, hand-annotated quality of the brand.

- **Do:** margin notes, annotations, pull quotes, a signature line, a single handwritten callout over an image, "take notes" on social frames.
- **Don't:** body copy, paragraphs, anything over roughly 10–12 words, navigation, labels, or UI text.
- Minimum weight is 400 — there is no light Caveat.
- Never fake-italicize it; it already reads as slanted script.

### Fonts With No Italic

**Bricolage Grotesque, Space Grotesk, Manrope, and Caveat have no italic variant.** A browser or design tool asked to italicize any of them will synthesize a skewed fake, which looks visibly wrong. In these families, emphasis comes from weight or color — never slant.

Real italics are available in Fraunces, DM Sans, IBM Plex Sans, IBM Plex Mono, and Instrument Serif.

### Utility / Labels / Captions

The utility face is **constant across all three categories** — it is part of the Take Stamp identity, not a category role.

```css
.utility-label {
  font-family: var(--font-utility); /* Space Mono */
  text-transform: uppercase;
  letter-spacing: 0.1em; /* within the 8–12% range */
}
```

Always uppercase, letter-spacing `+8%` to `+12%`.

### Loading

Safe import covering weight and italic axes only:

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Fraunces:ital,wght@0,100..900;1,100..900&family=Bricolage+Grotesque:wght@200..800&family=DM+Sans:ital,wght@0,100..1000;1,100..1000&family=Space+Grotesk:wght@300..700&family=IBM+Plex+Mono:ital,wght@0,400;0,500;0,600;1,400&family=IBM+Plex+Sans:ital,wght@0,100..700;1,100..700&family=Instrument+Serif:ital@0;1&family=Manrope:wght@200..800&family=Caveat:wght@400..700&family=Space+Mono:wght@400;700&display=swap" rel="stylesheet">
```

Loading all ten families at once is only for a surface that genuinely needs every category. **In production, load the one category's three families plus Caveat and Space Mono** — five families, not ten.

---

## Signature Motif: The Take Stamp

A small rotated rectangular tag — evokes a production slate or take marker. Recurring brand mark across assets.

**Spec:**
- Border: 1px, `--color-accent-cool` (Circuit teal)
- Background: `--color-surface` (Paper)
- Text: `--font-utility` (Space Mono, uppercase, tracked)
- Rotation: 2–4deg off-axis (not perfectly aligned — should feel hand-placed)

**The stamp keeps Space Mono in every category.** It is a fixed brand mark, so its type does not switch with Creative / Tech / Lifestyle — changing the stamp's face would change the mark itself.

```css
.take-stamp {
  display: inline-block;
  background: var(--color-surface);
  border: 1px solid var(--color-accent-cool);
  color: var(--color-text-primary);
  font-family: var(--font-utility);
  text-transform: uppercase;
  letter-spacing: 0.1em;
  padding: 4px 10px;
  transform: rotate(-3deg);
}
```

---

## Layout Specs (Social)

| Asset | Dimensions | Notes |
|---|---|---|
| Instagram carousel | 1080×1350px (4:5 portrait) | — |
| Reel cover | 1080×1920px | Safe zones: top 250px, bottom 400px — avoid text/key elements there (covered by platform UI) |

---

## Quick Reference — Do / Don't

**Do**
- Use the CSS variables above rather than hardcoding hex values.
- Keep Stone/Paper as the only backgrounds; Graphite/Slate as the only text colors.
- Reserve Signal amber for the single most important action or emphasis on a screen.
- Declare the type category explicitly (`data-daybook="tech"` etc.) rather than relying on the default — and load only that category's families.
- Use Caveat sparingly, as annotation over a frame, never as text.

**Don't**
- Reskin show key art (Alpha 8, etc.) with Daybook colors/type.
- Italicize Bricolage Grotesque, Space Grotesk, Manrope, or Caveat — none has an italic, so the result is a synthesized fake.
- Bold Instrument Serif — it ships at 400 only; faux-bold smears it. Scale it up instead.
- Mix families across categories in one composition (e.g. a Fraunces title over IBM Plex Sans body).
- Overuse Circuit teal as a fill color — it's a counterpoint accent, not a primary.

---

*Source of truth for Daybook brand specs. Part of the Bizzie Media Group brand system — see also the project's brand voice and canonical-facts documentation for non-visual brand guidance.*
