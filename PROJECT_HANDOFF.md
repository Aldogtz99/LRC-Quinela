# PROJECT HANDOFF — LRC Quiniela
**La Razita Club · FIFA World Cup 2026 Prediction App**
*Handoff Date: May 2026*

---

## 1. App Purpose

A shared web-based **quiniela (prediction game)** for a private friend group called La Razita Club, built around the FIFA World Cup 2026 (June 11 – July 19, 2026). Players predict match results across two phases, earn points as real results come in, and compete for a cash pot funded by buy-ins.

**How it works:**
- Phase 1: Predict all 48 group stage matches (1/X/2 + optional exact score) before the tournament starts
- Phase 2: Predict the full knockout bracket after the group stage ends
- Admin controls all windows, approvals, and result entry
- Top 3 players split the pot: 60% / 30% / 10%
- Buy-in: $50/player, pot and prizes update dynamically as players join

---

## 2. Current Stack

| Layer | Technology |
|---|---|
| Runtime | Claude Artifact (HTML + vanilla JS, single file) |
| Styling | Inline CSS + CSS custom properties |
| Fonts | Google Fonts: Bebas Neue, Oswald, Inter |
| Icons | Tabler Icons (CDN webfont) |
| Storage | `window.storage` (Claude artifact shared persistent storage) |
| Auth | PIN-based admin only (no player passwords) |
| Hosting | Claude artifact link (no external server needed) |
| Framework | None — pure HTML/CSS/JS |

**No npm, no build step, no backend.** The entire app is a single HTML artifact rendered inside Claude.ai. Shared storage syncs data across all users who open the same artifact.

---

## 3. Current File Structure

There is only one file — a Claude artifact rendered via `show_widget`. No files on disk.

The artifact contains:
```
<style>          CSS custom properties + all component styles
<html structure> Header, ticker, tabs, all screens as divs
<script>         All app logic, state management, storage calls
```

**Storage key:** `lrc_q_v7` (shared: true)

**State object shape:**
```js
{
  players: [{ name, status, pts, exactScores }],
  windows: { gs: bool, ko: bool },
  gRes: { [matchId]: { sh, sa, r, h, a } },
  preds: { [playerName]: { [matchId]: { r, sh, sa } } },
  locked: { [playerName]: bool },
  photos: { [playerName]: base64string }
}
```

**Admin PIN:** `1624`

---

## 4. Completed UI / Design Work

- ✅ Full landing page with hero split, tournament stats strip, How It Works, footer tag
- ✅ Player select screen with approved player list + join request flow
- ✅ Pending approval screen
- ✅ Admin login screen (PIN-based)
- ✅ Standings/leaderboard tab (dynamic player count, pot, prize amounts)
- ✅ My Picks tab (group stage predictions + knockout predictions)
- ✅ Rules tab (scoring tables + dynamic prize cards)
- ✅ Admin tab (windows, join requests, player management, result entry, recalculate)
- ✅ Player photo upload (base64, stored in shared storage)
- ✅ Toast notification system
- ✅ Dynamic ticker bar (player count, pot, window statuses)
- ✅ Responsive leaderboard with left-border rank indicators
- ✅ Prediction locking (per player, admin unlock)
- ✅ Group stage point calculation (result + exact score bonus)

---

## 5. Design System Summary

**Full design system:** see `LRC_Quiniela_Design_System.md`

**Visual direction:** Retro sports broadcast meets arcade tournament UI. Bold, clean, energetic, systemized.

### Colors
```css
--purple:  #5A1BFF   /* Primary brand, buttons, selected states */
--red:     #E31E24   /* Accent, alerts, header, phase 1 */
--lime:    #B6FF00   /* Highlight, success, CTA, points, active */
--dark:    #111111   /* Page background */
--dark2:   #1A1A1A   /* Panel background */
--dark3:   #222222   /* Row/item surface */
--dark4:   #2E2E2E   /* Hover surface */
--light:   #F7F7F7   /* Primary text */
--muted:   #A0A0A0   /* Secondary text, labels */
--border:  #333333
--border2: #444444
```

### Typography
- **Bebas Neue** — display numbers and headlines only
- **Oswald 600** — all UI labels, buttons, tabs, player names
- **Inter 400** — body copy, helper text only

### Key rules
- Dark backgrounds only — never white panels
- `border-radius: 2px` on everything
- Primary buttons always have trailing `›`
- Lime left accent bar on all panel titles
- No shadows, no gradients, no blobs, no confetti
- Halftone texture only on purple hero areas at `.06–.09` opacity

---

## 6. Current Components / Pages

### Screens
| Screen | ID | Status |
|---|---|---|
| Landing | `screen-landing` | ✅ Complete |
| Player Select | `screen-select` | ✅ Complete |
| Pending Approval | `screen-pending` | ✅ Complete |
| Admin Login | `screen-admin-login` | ✅ Complete |
| Main App | `screen-app` | ✅ Complete |

### Tabs (inside Main App)
| Tab | ID | Status |
|---|---|---|
| Standings | `tab-leaderboard` | ✅ Complete |
| My Picks | `tab-predictions` | ⚠️ Partial (4 sample groups only, KO is list-only) |
| Rules | `tab-rules` | ✅ Complete |
| Admin | `tab-admin` | ⚠️ Partial (group results only, no KO result entry) |

### Components (all inline, no separate files)
- Header + diagonal slash accent
- Ticker bar
- Tabs
- Landing hero split
- Stats strip
- How It Works grid
- Footer tag
- Leaderboard rows
- Stat boxes
- Player select buttons
- Match rows (1/X/2 + score inputs)
- Phase headers
- Panel + panel title with lime accent
- Badges (open/closed/pending)
- Info box
- Win card (admin window toggle)
- Player row (admin list)
- Prize cards
- Photo upload ring
- Toast notification
- Avatar (photo or initials)

---

## 7. Database / Auth Status

**Storage:** Claude `window.storage` with `shared: true`. All data lives in one JSON blob under key `lrc_q_v7`. Every user who opens the artifact reads and writes the same data.

**Limitations:**
- Last-write-wins — no conflict resolution
- No real-time push — users must refresh to see updates
- Base64 photos in storage count against the 5MB per-key limit
- No versioning or rollback

**Auth:**
- Admin: PIN `1624` (hardcoded in JS)
- Players: select their name from approved list — no password, no session token
- No impersonation protection beyond social trust (small friend group, acceptable)

---

## 8. Known Bugs / Unfinished Items

### Bugs
- [ ] Photo upload ring doesn't visually refresh after upload without a full tab re-render
- [ ] Score inputs in admin result entry don't re-populate correctly after `recalc()` without re-rendering the admin tab
- [ ] No validation preventing a player from submitting predictions with no picks at all (empty lock)
- [ ] If storage quota is exceeded by photos, save fails silently — no user feedback

### Unfinished Features
- [ ] **Only 4 of 12 groups built** — Groups A/B/C/D are sample data. All 12 real WC2026 groups with correct fixtures need to be loaded
- [ ] **Knockout bracket is a simple list** — Phase 2 shows round names but has no actual bracket structure. Players type winner names free-form, which is error-prone
- [ ] **No knockout result entry in admin** — Admin can enter group stage scores but cannot enter knockout round results or trigger KO point calculation
- [ ] **KO point calculation not implemented** — ET/PEN bonus scoring is collected but never calculated
- [ ] **No shareable link UX** — the app works via shared storage but there's no in-app flow to copy/share the artifact link
- [ ] **No phase transition messaging** — when admin closes Phase 1 and opens Phase 2, players get no notification
- [ ] **No tiebreaker logic** — the rules mention tiebreakers but they're not implemented in ranking

---

## 9. Next 10 Development Steps (In Order)

1. **Load all 12 real group stage fixtures** — replace the 4-group sample data with all 48 actual WC2026 group stage matches with correct team names and match IDs. Verify fixture data before building.

2. **Build knockout bracket prediction UI** — replace the free-text KO list with a structured bracket. Phase 2 should show actual R32 matchups (derived from entered group stage results or admin-set). Players pick the winner of each match.

3. **Build knockout result entry in admin** — add a KO results section to the admin tab matching the group stage result entry pattern. Each knockout match gets a score input + save button.

4. **Wire up KO point calculation** — implement `recalcKO()`: for each player, compare their knockout picks against actual results, apply round points, apply ET/PEN bonuses, add to group stage total.

5. **Add empty-prediction guard on lock** — before locking, check that the player has made at least one prediction. Warn if fewer than 50% of open matches have a result picked.

6. **Add photo storage size guard** — before saving a photo, check estimated storage usage. If near 4MB, warn the user and optionally compress the image (canvas resize to max 200×200px before base64).

7. **Add phase transition notice** — when the admin opens Phase 2, show a banner to players on next load: "Group stage is over — the knockout bracket is now open for predictions."

8. **Implement tiebreaker sorting** — update leaderboard sort: first by `pts` desc, then by `exactScores` desc, then by correct KO picks desc.

9. **Add shareable link section** — add a small info panel (in admin and/or rules tab) that explains how to share the artifact, with a copy-link button using `window.location.href`.

10. **End-to-end test with real users** — before the tournament starts, run a full test: have 2–3 friends join, submit predictions, lock them, enter some fake results, verify points calculate correctly across both phases.

---

## 10. Important Rules for New Claude Sessions

```
⚠️  DO NOT redesign the app unless the user explicitly asks.
⚠️  DO NOT change colors, fonts, spacing, or component styles unless asked.
⚠️  Follow LRC_Quiniela_Design_System.md for ALL visual decisions.
⚠️  Make small, targeted changes only — one feature at a time.
⚠️  Always preserve the existing storage key (lrc_q_v7) and state shape.
⚠️  Never change the admin PIN (1624) unless asked.
⚠️  When adding new components, match the existing component patterns exactly.
⚠️  Test logic changes mentally before applying — the app has no undo.
⚠️  If in doubt about a visual decision, ask before implementing.
⚠️  The app is a single HTML artifact — keep it that way unless asked to change.
```

---

## 11. Quick Context for New Claude

- This is a **friend group World Cup betting pool**, not a commercial app
- The group is called **La Razita Club (LRC)**
- The admin is the person who organized the pool — they control everything
- Players are trusted friends — no hostile users, minimal security needed
- The tournament runs **June 11 – July 19, 2026**
- The World Cup has **48 teams, 12 groups, 104 total matches**
- The app must be ready before **June 11, 2026**
- Design was finalized after several iterations — do not revisit it without being asked
- The user has a separate `LRC_Quiniela_Design_System.md` file that is the authoritative design reference

---

*End of handoff document.*
