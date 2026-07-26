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

```css
:root {
  --font-display: "Bricolage Grotesque", sans-serif; /* 700–800 weight only, no italic exists */
  --font-body: "Archivo", sans-serif;                 /* 400–600 weight, has real italic */
  --font-utility: "Space Mono", monospace;             /* labels/utility, always uppercase */
}
```

| Role | Font | Weight | Notes |
|---|---|---|---|
| Display / headlines | Bricolage Grotesque | 700–800 | **No italic variant exists in this family** — never fake-italicize it |
| Body copy | Archivo | 400–600 | Real italic available — use for in-body emphasis |
| Utility / labels / captions | Space Mono | 400 | Always `text-transform: uppercase`, letter-spacing `+8% to +12%` |

```css
.utility-label {
  font-family: var(--font-utility);
  text-transform: uppercase;
  letter-spacing: 0.1em; /* within the 8–12% range */
}
```

---

## Signature Motif: The Take Stamp

A small rotated rectangular tag — evokes a production slate or take marker. Recurring brand mark across assets.

**Spec:**
- Border: 1px, `--color-accent-cool` (Circuit teal)
- Background: `--color-surface` (Paper)
- Text: `--font-utility` (Space Mono, uppercase, tracked)
- Rotation: 2–4deg off-axis (not perfectly aligned — should feel hand-placed)

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

**Don't**
- Reskin show key art (Alpha 8, etc.) with Daybook colors/type.
- Italicize Bricolage Grotesque (no italic exists — fallback would fake it and look wrong).
- Overuse Circuit teal as a fill color — it's a counterpoint accent, not a primary.

---

*Source of truth for Daybook brand specs. Part of the Bizzie Media Group brand system — see also the project's brand voice and canonical-facts documentation for non-visual brand guidance.*
