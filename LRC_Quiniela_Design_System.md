# LRC Quiniela — Design System & Style Guide
**La Razita Club · World Cup 2026**
*Version 1.0 — May 2026*

---

## 1. Design Principles

The LRC Quiniela app should feel like a **retro sports broadcast meets arcade tournament UI**. Every decision — color, type, spacing, motion — should serve these four adjectives:

- **Bold** — high contrast, strong hierarchy, no timid choices
- **Clean** — restraint in decoration, every element earns its place
- **Energetic** — the UI should feel alive without being chaotic
- **Systemized** — motifs repeat consistently; nothing looks accidental

**The one rule to remember:** if you wouldn't see it on a stadium scoreboard or a 90s ESPN lower-third, question whether it belongs here.

---

## 2. Color System

### Core Palette

| Token | Hex | Role |
|---|---|---|
| `--purple` | `#5A1BFF` | Primary brand, main interactive color |
| `--purple2` | `#7040FF` | Purple hover state |
| `--red` | `#E31E24` | Accent, alerts, destructive, phase 1 |
| `--red2` | `#FF3A3F` | Red hover state |
| `--lime` | `#B6FF00` | Highlight, success, active states, CTA |
| `--lime2` | `#CCFF33` | Lime hover state |
| `--dark` | `#111111` | Page background |
| `--dark2` | `#1A1A1A` | Panel/card background |
| `--dark3` | `#222222` | Elevated surface (inputs, rows) |
| `--dark4` | `#2E2E2E` | Highest surface (hover states) |
| `--light` | `#F7F7F7` | Primary text, icons on dark |
| `--muted` | `#A0A0A0` | Secondary text, labels, metadata |
| `--border` | `#333333` | Default borders |
| `--border2` | `#444444` | Elevated borders |

### Color Usage Rules

**Purple** is the primary action color. Use it for: primary buttons, selected states (1/X/2 picks), phase headers, avatar backgrounds, leaderboard progress bars, the hero left panel.

**Red** is the accent. Use it for: the header, alert states, phase 1 numbering, the "01" how-it-works step, destructive buttons (reject, remove), closed status badges.

**Lime** is the reward color. Use it for: active/success states, the lime border accent on panel titles, leaderboard points, prize amounts, locked-in confirmation, the "Open" badge, CTA buttons, ticker dots, the "03" how-it-works step.

**Never use lime as a background for large areas** — it's an accent only. The one exception is the landing page right panel (the stats/buttons block).

**Dark backgrounds only.** Never use white or light gray as a page or panel background. Light (`#F7F7F7`) is for text and icons only.

### Semantic Colors

| State | Color | Usage |
|---|---|---|
| Success / Locked | `--lime` | Confirmed predictions, approved players |
| Warning / Pending | `#A080FF` (light purple) | Pending requests, knockout phase badge |
| Error / Destructive | `--red` | Rejections, removals, closed status |
| Neutral | `--muted` | Labels, helper text, disabled states |

---

## 3. Typography System

### Font Stack

```css
--font-d: 'Bebas Neue', sans-serif;       /* Display / Headlines */
--font-s: 'Oswald', sans-serif;           /* Sub-headlines / UI labels */
--font-b: 'Inter', sans-serif;            /* Body / helper text */
```

### Type Scale

| Role | Font | Size | Weight | Letter-spacing | Color |
|---|---|---|---|---|---|
| Hero title (LA RAZITA) | Bebas Neue | 3.5rem | — | `.08em` | `--light` |
| App title (QUINIELA) | Bebas Neue | 2.2rem | — | `.15em` | `--light` |
| Panel title | Bebas Neue | 1.1rem | — | `.12em` | `--lime` |
| Leaderboard points | Bebas Neue | 1.6rem | — | `.06em` | `--lime` |
| Stat numbers | Bebas Neue | 1.5rem | — | `.06em` | varies |
| How-it-works numbers | Bebas Neue | 2.5rem | — | `.08em` | red/purple/lime |
| Section label | Oswald | .72rem | 600 | `.12em` | `--muted` |
| Button text | Oswald | .9rem | 600 | `.1em` | — |
| Tab text | Oswald | .85rem | 600 | `.1em` | — |
| Player name | Oswald | .95rem | 600 | `.05em` | `--light` |
| Ticker text | Oswald | .75rem | 600 | `.08em` | `--light` |
| Badge text | Oswald | .68rem | 600 | `.08em` | — |
| Body / helper | Inter | .82rem | 400 | normal | `--muted` |
| Small metadata | Inter | .72rem | 400 | normal | `--muted` |

### Typography Rules

1. **Bebas Neue is for numbers and display only.** Never use it for full sentences or paragraph text.
2. **Oswald is for all interactive UI text** — buttons, tabs, labels, player names, section headers.
3. **Inter is for explanatory text only** — how-it-works body copy, helper text, info boxes, rules descriptions.
4. **All caps is enforced on Oswald** via `text-transform: uppercase` and `letter-spacing: .08em` minimum.
5. **Never mix font sizes within the same hierarchy level.** A section label is always `.72rem`. A panel title is always `1.1rem`. Consistency is the system.

---

## 4. Spacing System

Use a base-8 spacing scale. All padding and gap values should be multiples of 4px.

| Token | Value | Usage |
|---|---|---|
| `xs` | 4px | Icon gaps, tight internal spacing |
| `sm` | 8px | Component internal padding |
| `md` | 12px | Default gap between related items |
| `lg` | 16px (1rem) | Section internal padding |
| `xl` | 20px (1.25rem) | Panel padding |
| `2xl` | 24px (1.5rem) | Page padding |
| `3xl` | 32px (2rem) | Between major sections |

**Page content padding:** `1.25rem` on all sides.
**Panel internal padding:** `1.25rem`.
**Match row padding:** `.6rem .9rem`.
**Ticker padding:** `.4rem 1.25rem`.

---

## 5. Component Library

### 5.1 Buttons

Three tiers, each with a specific purpose:

**Primary Button** — `btn-primary`
```
Background: --purple
Text: --light
Border: 2px solid --purple
Font: Oswald 600 .9rem
Trailing chevron: › (mandatory)
Width: stretch to container when solo
Use for: main action per screen (Lock Predictions, Enter, I'm a Player)
```

**Secondary Button** — `btn-secondary`
```
Background: transparent
Text: --light
Border: 2px solid --light
Font: Oswald 600 .9rem
No chevron
Use for: alternate action (Admin login on lime bg uses dark border/text)
```

**Lime CTA Button** — `btn-lime`
```
Background: --lime
Text: --dark
Border: 2px solid --lime
Font: Oswald 600 .9rem
Trailing chevron: ›
Use for: positive admin actions (Open window, Recalculate, Approve)
```

**Ghost Button** — `btn-ghost`
```
Background: transparent
Text: --muted
Border: 1px solid --border2
Font: Oswald 600
Hover: text becomes --light, border becomes --light
Use for: secondary navigation (Back, Save draft, Unlock)
```

**Danger Button** — `btn-danger`
```
Background: transparent
Text: --red
Border: 1px solid --red
Font: Oswald 600
Use for: destructive actions (Remove, Reject)
```

**Small variant:** append `.btn-sm` — reduces padding to `.35rem .75rem`, font-size to `.78rem`.

**Button rules:**
- Every primary button has a trailing `›` character, no exceptions.
- Buttons are `border-radius: 2px` — sharp corners are part of the system.
- Never use `border-radius` higher than 4px on any interactive element.
- Disabled state: `opacity: 0.35`, `cursor: not-allowed`.

---

### 5.2 Panels (Cards)

```css
.panel {
  background: var(--dark2);        /* #1A1A1A */
  border: 1px solid var(--border); /* #333 */
  border-radius: 2px;
  padding: 1.25rem;
  margin-bottom: .75rem;
}
```

**Panel title** always includes a 3px lime left accent bar:
```html
<div class="panel-title">
  <span style="display:block;width:3px;height:1em;background:var(--lime)"></span>
  Title Text
</div>
```

Panels are never white. Nested surfaces inside panels use `--dark3` (`#222`).

---

### 5.3 Match Row

The fundamental data unit of the app:

```
Background: --dark3
Border: 1px solid --border
Border-radius: 2px
Padding: .6rem .9rem
Layout: grid 3 columns — [team names | score inputs | result buttons]
```

**Result buttons (1/X/2):**
- Default: `--dark4` background, `--border2` border, `--muted` text
- Selected: `--purple` background, `--purple` border, `--light` text
- Font: Bebas Neue `.95rem`
- Shape: `border-radius: 2px`

**Score inputs:**
- Width: `32px`
- Text-align: center
- Background: `--dark4`

---

### 5.4 Leaderboard Row

```
Layout: grid 4 columns — [rank | avatar | name+meta | points]
Background: --dark3
Border: 1px solid --border
Border-left: 3px solid [rank color]  ← the key design detail
Border-radius: 2px
```

Rank colors:
- 1st: `--lime` (`#B6FF00`)
- 2nd: `--muted` (`#A0A0A0`)
- 3rd: `#C08040` (bronze)
- Others: `transparent`

Points column: Bebas Neue `1.6rem`, color `--lime`.
Progress bar: `3px` height, `--border` background, `--purple` fill.

**Never use background color fills to differentiate rank** — the left border is the only rank indicator.

---

### 5.5 Stat Box

```
Background: --dark3
Border: 1px solid --border2
Border-radius: 2px
Padding: .6rem .9rem
Layout: column, centered
Value: Bebas Neue 1.5rem
Label: Oswald 600 .65rem uppercase --muted
```

Stat boxes live in a flex row with `gap: .5rem` and `flex-wrap: wrap`.

---

### 5.6 Phase Header

Used to introduce prediction sections:

```
Background: --purple
Border-left: 3px solid --lime
Padding: .5rem 1rem
Font: Bebas Neue .95rem letter-spacing .12em
Contains: [phase label left | status badge right]
```

---

### 5.7 Badges

```
Font: Oswald 600 .68rem uppercase letter-spacing .08em
Padding: .15rem .5rem
Border-radius: 2px
Border: 1px solid [semantic color]
```

| Badge | Background | Text | Border |
|---|---|---|---|
| Open | `rgba(182,255,0,.15)` | `--lime` | `--lime` |
| Closed | `rgba(227,30,36,.12)` | `--red` | `--red` |
| Pending | `rgba(90,27,255,.2)` | `#A080FF` | `#7050DD` |

Badge count (notification dot):
```
Background: --red
Color: white
Border-radius: 50%
Size: 17px × 17px
Font: Inter 700 .68rem
```

---

### 5.8 Info Box

```
Background: --dark3
Border-left: 3px solid --purple (default) or --lime (success) or --red (error)
Padding: .65rem 1rem
Font: Inter .82rem
Color: --muted (default) or --lime (success)
Margin-bottom: 1rem
Border-radius: 0 (left border only)
```

---

### 5.9 Avatar

Two states — photo uploaded, or initials fallback:

```
Shape: border-radius: 50%
Default size: 36px (leaderboard), 38px (player select), 44px (profile header)
Photo: object-fit: cover
Initials: Oswald 600, font-size = size × 0.32, background from player color array
```

Player color array (assigned in join order):
```
#5A1BFF, #E31E24, #2a8a00, #1A4B9B, #c07010, #0a7a6a,
#a02060, #0a6a9a, #7a1a7a, #3a6a10, #8B3FE8, #c83030,
#006B3F, #c8a000, #2a4a9a, #9a3a20
```

---

### 5.10 Ticker Bar

```
Background: --dark
Border-top: 2px solid --lime
Border-bottom: 2px solid --lime
Padding: .4rem 1.25rem
Layout: flex row, gap 1.5rem
```

Each item: `icon (lime, .85rem) + Oswald 600 .75rem uppercase`.
Separator between items: `◆` in `--border2`.

---

### 5.11 Win Card (Admin Window Toggle)

```
Background: --dark3
Border: 1px solid --border
Border-radius: 2px
Padding: .85rem 1rem
Layout: flex row, space-between
Title: Oswald 600 .9rem --light
Subtitle: Inter .72rem --muted
Right side: [badge + button]
```

---

### 5.12 Section Label

```
Font: Oswald 600 .72rem
Letter-spacing: .12em
Text-transform: uppercase
Color: --muted
Margin-bottom: .5rem
```

Used above groups of related items (match groups, player lists, etc.).

---

### 5.13 Tabs

```
Background: --dark2
Border-bottom: 2px solid --border
Font: Oswald 600 .85rem uppercase letter-spacing .1em
Default color: --muted
Active color: --lime
Active indicator: border-bottom 3px solid --lime, margin-bottom -2px
Hover: --light
Padding: .75rem 1.1rem
```

---

### 5.14 Form Inputs

```
Background: --dark3
Border: 1px solid --border2
Border-radius: 2px
Color: --light
Font: Inter .875rem
Padding: .5rem .75rem
Focus border: --lime
```

Score inputs are `32px` wide, centered text.

---

## 6. Decorative Graphics Rules

The design uses three decorative motifs, each with strict rules on where and how to apply them:

### 6.1 Halftone Dot Texture

```css
background-image: radial-gradient(circle, rgba(255,255,255,.07) 1px, transparent 1px);
background-size: 7px 7px;
```

**Use on:** Hero left panel (purple), header background, any large purple background section.
**Never use on:** Dark panels, match rows, form areas, anywhere information density is high.
**Opacity rule:** Always `rgba` with `.06–.09` alpha. Never full opacity dots.

### 6.2 Diagonal Color Slash

Used in the header top-right corner only:

```css
background: linear-gradient(135deg, var(--red) 0%, var(--red) 50%, var(--lime) 50%, var(--lime) 100%);
clip-path: polygon(40% 0, 100% 0, 100% 100%, 60% 100%);
position: absolute; top: 0; right: 0; width: 120px; height: 100%;
```

**Use only in the main header.** One instance per page. Never replicate elsewhere.

### 6.3 Left Accent Bar

A 3px vertical bar in `--lime`, used to signal a section title or phase boundary:

```css
width: 3px;
height: 1em;  /* or 100% for full-height borders */
background: var(--lime);
display: block;
```

**Use on:** Panel titles, phase headers (as `border-left`), leaderboard row rank indicators.
**Color variants:** Lime for panel titles and success; purple for info boxes; red for warnings.

### 6.4 What NOT to do

- No drop shadows anywhere
- No gradient fills on panels or buttons
- No circular blob shapes (removed from previous version)
- No random confetti, sparkle, or star decorations
- No SVG illustrations that aren't part of a defined system
- No border-radius above 4px on any element
- No full-bleed images or photo backgrounds

---

## 7. Background Treatment Rules

### Page background
Always `--dark` (`#111111`). No exceptions.

### Surface hierarchy (light to dark = deeper = more elevated)

```
Page:     --dark   #111  (deepest, furthest back)
Panel:    --dark2  #1A1A (cards, major sections)
Row/Item: --dark3  #222  (match rows, player rows, stat boxes)
Hover:    --dark4  #2E2E (interactive hover state)
```

The hierarchy goes **darker = further back, lighter = closer to user**. A hovered match row (`--dark4`) sits "on top of" the panel background (`--dark2`). Never invert this.

### Colored background sections

Only four colored backgrounds are permitted for full sections:

| Section | Color | When |
|---|---|---|
| Header | `--purple` + halftone texture | Always |
| Hero left panel | `--purple` + halftone + gradient overlay | Landing only |
| Hero right panel | `--lime` | Landing only |
| Stats strip blocks | Alternating `--red`, `--dark2`, `--purple`, `--dark3` | Landing only |

All other sections default to the dark surface hierarchy.

### Borders

All borders are `1px solid --border` (`#333`) by default.
Interactive borders on focus/hover: `--lime`.
Rank borders on leaderboard: `3px solid [rank color]`.
Phase headers: `border-left: 3px solid --lime`.

---

## 8. Motion & Animation Direction

### Principles

The app currently has no animation. When adding motion, follow these rules:

1. **Motion should confirm, not decorate.** Animate when something changes state — not to make the page feel "alive."
2. **Fast in, fast out.** Transitions: `150ms` for micro (hover, focus). `250ms` for state changes. `400ms` max for anything reveal-based.
3. **Easing:** `ease-out` for entrances (things arriving). `ease-in` for exits (things leaving). `ease-in-out` for state toggles.
4. **No bouncing, no springs, no elastic.** This is a broadcast UI, not a consumer app.

### Approved animations

**Button hover:** `background-color` transition, `150ms ease-out`. No transform.

**Toast notification:**
```css
opacity: 0 → 1;
transform: translateY(8px) → translateY(0);
transition: all 250ms ease-out;
```

**Tab switch:** Instant — no animation. Tab content appears immediately.

**Leaderboard bar:**
```css
width: 0 → N%;
transition: width 400ms ease-out;
transition-delay: 100ms;
```
Apply when leaderboard first renders, not on every re-render.

**Score update (when admin enters results):**
Points value should flash lime briefly:
```css
@keyframes scoreFlash {
  0%   { color: var(--lime); }
  50%  { color: var(--light); }
  100% { color: var(--lime); }
}
animation: scoreFlash 600ms ease-in-out;
```

**Prediction lock confirmation:**
The player profile card border briefly flashes lime: `border-color` from `--border` → `--lime` → `--border`, `500ms`.

**Phase header reveal (when a window opens):**
```css
opacity: 0 → 1;
transform: translateX(-8px) → translateX(0);
transition: all 300ms ease-out;
```

### Do not animate

- Layout shifts (no width/height transitions on panels)
- Color changes on text (except scoreFlash above)
- Scroll position
- The ticker bar — it is always static

---

## 9. Screen-by-Screen UI Guide

### 9.1 Landing Screen

**Structure (top to bottom):**
1. Header (purple + halftone + diagonal slash)
2. Ticker (dark + lime borders)
3. Hero split (purple left | lime right)
4. Stats strip (4 colored blocks)
5. How It Works (dark2 + 3-column grid)
6. Footer tag (dark2, "Play. Compete. **Bragging Rights.**")
7. Leaderboard preview (appears once players join)

**Key rules:**
- Footer tag is always present, even with no players
- Leaderboard preview shows maximum 5 players
- The lime right panel must always show 3 stat rows + 2 buttons

### 9.2 Player Select Screen

**Structure:**
1. Back button (ghost)
2. Single panel: "Who are you?"
3. Approved player list (ps-btn rows)
4. Divider
5. Request to join (input + lime button)

**Key rules:**
- Player rows show avatar + name + submission status
- "✓ Predictions submitted" in `--lime`; "Predictions pending" in `--muted`

### 9.3 My Picks Screen (Predictions)

**Structure:**
1. Player profile bar (dark2 panel, photo upload, name, status)
2. Info box (locked confirmation OR window-closed notice)
3. Phase 1 header + group sections (if open or previously submitted)
4. Phase 2 header + knockout rows (if open or previously submitted)
5. Lock / Save draft buttons (if window open and not locked)

**Key rules:**
- Phase headers are always purple with lime left border
- Group label is a section-label above each group's matches
- 1/X/2 buttons: selected state is purple fill
- Score inputs sit between the team names and result buttons
- Lock button is primary (purple with ›); save draft is ghost

### 9.4 Standings Screen (Leaderboard)

**Structure:**
1. Stat row (Players, Pot, 1st/2nd/3rd prizes — dynamic)
2. Leaderboard rows (sorted by points desc)

**Key rules:**
- Rank 1 row: `border-left: 3px solid --lime`, background `#1a1f00`
- Rank 2: `border-left: 3px solid --muted`
- Rank 3: `border-left: 3px solid #c08040`
- Medal emojis (🥇🥈🥉) are the rank display for top 3
- Prize amount shown inline next to name in `--lime`, `.7rem` Oswald
- All stat values are dynamic — recalculate when player count changes

### 9.5 Rules Screen

**Structure:**
1. Panel title (Bebas Neue, lime accent bar)
2. 2-column grid: Phase 1 table | Phase 2 table
3. Prize distribution panel (3-column prize cards)
4. Tiebreaker note

**Key rules:**
- Point values always in Bebas Neue `1rem` lime
- Tables use `1px solid --border` row dividers only, no column dividers
- Prize cards: lime border (1st), muted (2nd), bronze (3rd)
- Prize amounts update dynamically based on current player count

### 9.6 Admin Panel

**Structure:**
1. Panel title
2. Stat row (Players, Pot, Pending)
3. Prediction Windows panel (2 win-cards with toggle buttons)
4. Join Requests panel (approve/reject rows)
5. Players panel (list with unlock/remove actions)
6. Enter Results panel (match rows with score inputs + save buttons)
7. Recalculate All Points button (lime CTA)

**Key rules:**
- Pending count badge is red when > 0
- "Open" window button is lime; "Close" is ghost
- Approve button is `btn-approve` (lime); reject/remove is `btn-danger` (red outline)
- Result entry uses same match-row component as predictions view
- Recalculate button always at the bottom of result entry, full accessible

---

## 10. CSS Variable Quick Reference

Paste this block at the top of any new screen or component to maintain consistency:

```css
:root {
  /* Colors */
  --purple:  #5A1BFF;
  --purple2: #7040FF;
  --red:     #E31E24;
  --red2:    #FF3A3F;
  --lime:    #B6FF00;
  --lime2:   #CCFF33;
  --dark:    #111111;
  --dark2:   #1A1A1A;
  --dark3:   #222222;
  --dark4:   #2E2E2E;
  --light:   #F7F7F7;
  --muted:   #A0A0A0;
  --border:  #333333;
  --border2: #444444;

  /* Typography */
  --font-d: 'Bebas Neue', sans-serif;
  --font-s: 'Oswald', sans-serif;
  --font-b: 'Inter', sans-serif;
}
```

---

## 11. Do / Don't Checklist

### ✅ Always Do

- Use `border-radius: 2px` on all components
- Include the trailing `›` on all primary and lime buttons
- Apply `letter-spacing: .08em` minimum on all Oswald text
- Use the lime left accent bar on all panel titles
- Keep background surfaces in the dark hierarchy (`--dark` → `--dark2` → `--dark3` → `--dark4`)
- Use Bebas Neue only for display numbers and headlines
- Use Inter only for body/helper text
- Keep halftone texture at `.06–.09` opacity only

### ❌ Never Do

- Use white or light backgrounds for panels or page surfaces
- Use `border-radius` above 4px
- Add drop shadows or glow effects
- Use gradients on buttons or panels
- Add decorative blobs, circles, or random shapes
- Use Bebas Neue for paragraph text or instructions
- Mix hierarchy levels (don't put a `--dark3` element directly on `--dark`, skipping `--dark2`)
- Animate layout dimensions (width/height of panels)
- Use more than three font families
- Use colors outside the defined palette

---

*LRC Quiniela Design System v1.0 — Reference this document before building any new screen or component.*
