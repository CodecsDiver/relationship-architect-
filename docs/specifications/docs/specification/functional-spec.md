# Daniel & Veronica's Relationship Architecture
## Program Framework, Form & Features
### Prototype 1 — July 2026

---

## Overview

A shared web application that functions as a living record of a couple's relationship — their values, governance meetings, goals, risks, decisions, and long-term vision. Built as a single HTML file, fully offline-capable via localStorage, with no login required.

**Tagline:** Designed to grow. Built on love.
**Signature quote:** "We're not just building a relationship. We're architecting a life we love."

---

## Brand Identity

| Element | Value |
|---|---|
| Background | `#060B14` (near-black navy) |
| Panel surface | `#08101E` |
| Primary accent | `#C9A451` (gold) |
| Secondary accent | `#D4847A` (rose) |
| Text | `#E8DECE` (warm off-white) |
| Display typeface | Cormorant Garamond (serif — editorial) |
| Label/mono typeface | JetBrains Mono |
| Logo | "DV" monogram in gold serif, rose-pink heart overlapping the V, inside a thin gold circle |

---

## Themes (9 total)

1. **Midnight Gold** — Near-black navy bg, gold + rose accents (default/brand)
2. **Warm Ember** — Dark brown bg, warm gold + terracotta
3. **Cool Slate** — Near-black blue bg, cool steel blue accents
4. **Monochrome** — Pure black bg, white/grey accents
5. **Dracula** — Dark purple bg, violet + pink accents
6. **Neon** — Pure black bg, electric green + hot pink
7. **Pastel** — Deep purple bg, lavender + blush
8. **Vanilla Walnut** — Dark walnut bg, orange + turquoise (Vee's palette 1)
9. **Olive Saffron** — Olive leaf bg, deep saffron + maroon (Vee's palette 2)

Theme selection via dropdown in topbar. Selection persists in localStorage.

---

## Application Shell

### Top Bar (persistent)
- **Left:** DV logo mark (clickable → home), app title `</> relationship.architecture`, subtitle `Daniel & Veronica`
- **Center:** SoundCloud media player button (opens Dan Tanner's SoundCloud in new tab)
- **Right:** Theme picker dropdown, connection status badge

### Sidebar (persistent, left)
- Dashboard home link
- All 11 section tabs (icon + label, active state highlighted in gold, left border accent)
- Custom file tabs indented under their parent section
- "+ Add File" at bottom (dashed rose border, distinct from fixed sections)

### Content Area (scrollable, right)
- All section content renders here
- Background: near-black with subtle DV watermark

---

## Home Dashboard

- Grid of 11 cards (one per section)
- Each card shows: icon, section name, italic motto, progress bar (% fields filled), entry count (x/y), percentage
- Progress bar: gold → rose gradient
- Clicking a card opens that section
- "+ Add File" footer at bottom of dashboard
- Data: completion percentage calculated from localStorage field values

---

## Section Template (shared by all 11 sections)

**Header:** Icon + section name + italic motto

**Toolbar:**
- **Save** — persists all field values to localStorage, shows toast "✓ Saved"
- **✏️ Edit / 🔒 Lock** — toggles read-only vs. editable mode (sections start locked)
- **Export** — downloads section as `.txt` file
- **Close** — returns to home dashboard
- **Delete** — two-step confirmation modal (cannot be undone); clears content for built-in sections, fully removes custom sections

**Add File footer** — dashed rose border at bottom of every section, opens Add File modal pre-set to that section as parent

---

## The 11 Sections

### 1. Executive Summary
5 free-text prompts: Purpose, Mission Statement, Vision Statement, Success Definition, Relationship Philosophy.

### 2. Guiding Principles
- 🔒 **Seeded (locked):** 8 core principles displayed as a fixed reference list — Love Before Ego, Radical Honesty, Team Over Individual, Attack Problems Not People, Continuous Improvement, Assume Positive Intent, Protect Trust at All Costs, Grace Over Perfection
- 1 open field: Additional Principles

### 3. Core Values
17 labeled sub-fields across 4 groups:
- Love & Respect (Definition, Behaviors, Anti-Patterns, Examples)
- Communication (Definition, Expected Behaviors, Meeting Rules, Conflict Rules)
- Trust (How It's Built, How It's Repaired, Violations)
- Growth (Learning, Health, Spiritual, Career, Financial, Relationship)

### 4. System Architecture
- **Constellation visualization** — animated canvas with 12 orbital nodes
- **Interactive canvas features:**
  - Twinkling background star particle system (90 stars, randomized fade cycles)
  - Shooting stars (randomized timing, trailing glow)
  - Orbs drift toward mouse with slight orbital motion (magnetic attraction)
  - Click an orb → zoom into it (canvas scale 2.2×, smooth lerp transition)
  - Popup appears at click coordinates showing module name, 3 sub-items, "Add file" button
  - Close popup (✕) → canvas zooms back out
  - Orb glow pulses with sine wave animation; active orb has stronger halo
  - Center DV node pulses gold, rose heart, "ARCHITECTURE" label
- **Module cards grid** — 12 cards below the constellation, one per module, each with color-coded dot, name, 3 sub-items listed, and an "Add file to [Module]" button
- **12 modules:** Foundation, Communication, Emotional Health, Physical Health, Finances, Home, Family, Adventure, Intimacy, Conflict Resolution, Future Planning, Legacy

### 5. Weekly Governance Meeting
Fully structured page (render function written, wiring in progress):
- Meeting date + week number
- Check-in cards (Daniel / Veronica side by side): Mood/Energy/Stress sliders (1–10), Win of the Week, Struggle of the Week
- Appreciation exchange: 3 gratitude fields each direction
- Open Issues free text
- Action Items table (Task / Owner / Status / Notes, add/delete rows)
- Weekly Metrics table: 8 metrics rated 1–10 by both partners with live average bar (Overall, Communication, Intimacy, Stress, Financial, Physical, Spiritual, Fun)
- Seeded ADR-001 example (locked, visually distinct)
- Decision Log (ADR) table: add/delete rows (Date / Decision / Reasoning / Outcome)
- New Goals by horizon: Daily / Weekly / Monthly / Yearly / Lifetime text areas

### 6. Goals Architecture
Reference field + repeatable goals table (Goal / Milestone / Tasks / Owner / Deadline / Status).

### 7. Long-Term Roadmap
5 horizon text fields: 1 Year, 5 Years, 10 Years, Retirement, Legacy.

### 8. Risk Register
- 🔒 **Seeded table (locked, visually distinct):** 7 pre-loaded risks (Financial Stress, Poor Communication, Burnout, Family Conflict, Health Issues, Career Instability, Emotional Distance) — each with Likelihood / Impact / Mitigation columns, lock icon per row, dashed gold "SEEDED EXAMPLES" banner
- 1 open field: Additional Risks

### 9. Decision Log
Repeatable table: Date / Decision / Reasoning / Outcome. Starts empty.

### 10. Meeting Notes
Repeatable dated entries: Date / Week # / Topics / Notes / Action Items.

### 11. Appendix
6 fields: Books & Resources, Daniel's Dreams, Veronica's Dreams, Bucket List, Quotes (pre-filled with signature quote), Anniversaries & Important Dates.

---

## Seeded Content System

Seeded/example content is visually distinguished from user-entered content:
- **Dashed gold banner:** "🔒 SEEDED EXAMPLES — These rows are pre-loaded starting points. They are locked and separate from your real data."
- **Row styling:** dimmed, italic text, gold left border, lock icon in final column
- **Locked reference lists** (Guiding Principles): gold header bar with lock icon, italic dimmed text per item
- User-entered content: normal weight, full opacity, no lock

---

## Custom Files (Add File)

- **Trigger:** "Add File" button in sidebar, each section's footer, or dashboard footer
- **Modal:** Floating window with title bar, name input, layout picker (Blank / Clone), Create button
- **Storage:** custom sections saved to `dv_custom_sections` in localStorage
- **Parent binding:** new file is bound to the section whose "Add File" button was clicked; appears indented under that section in sidebar
- **Document editor:** Opens as a floating window (macOS-style traffic light, DV logo in header, title, full-width textarea, Save & Close button, Export + Delete at bottom)
- **Delete:** opens two-step confirmation modal, removes from sidebar and localStorage
- **System Architecture special case:** "Add file to [Module]" button pre-populates the text file with that module's 3 sub-items as bullet points

---

## Data Persistence

- All data stored in browser `localStorage`
- Keys: `dv_sec_[sectionId]` per section, `dv_custom_sections` for custom file list, `dv_theme` for selected theme
- Save is immediate on button click — no auto-save
- Data is per-browser; not shared between devices in Prototype 1
- No login, no server, no database in Prototype 1

---

## Delete Confirmation System

All destructive actions use a custom in-app modal (not browser `confirm()`, which is blocked in iframes):
- Modal floats center-screen with backdrop blur
- Two buttons: Cancel / confirm action (rose-tinted)
- Auto-dismissed on cancel or backdrop click

---

## Media Player

- Button in topbar opens Dan Tanner's SoundCloud page in a new tab
- SoundCloud icon + artist name + "▶ OPEN PLAYLIST" label
- Hovering highlights gold border

---

## Toast Notifications

- Bottom-right, gold→rose gradient background
- Auto-dismisses after 2.8 seconds
- Used for: Save confirmation, Export confirmation, File created, Deleted/Cleared

---

## Loading Screen

- Shown on app init while localStorage loads
- Spinner + "CONNECTING TO DATABASE..." label
- Dismissed instantly once data is ready (no network wait in Prototype 1)

---

---

# Future Build — Planned Updates (Prototype 2)

## Gamification System
- XP bar + level number displayed persistently in topbar
- Daily streak badge (🔥 + count) and weekly streak badge (⚡ + count) in topbar
- XP progression pace to be carefully designed (not too fast, not too slow)
- Level unlocks to be defined (cosmetic rewards, new features, etc.)
- XP is shared between Daniel and Veronica — requires cloud sync
- Streak resets on missed day/week; XP is never removed

## Shared Cloud Storage (Firebase)
- Reintroduce Firebase Firestore for real-time sync
- Both partners see the same data across devices
- Device recognition
- "Last edited by" indicator per section
- XP and streaks shared and synced

## Weekly Governance — Wiring
- Connect the fully-written `renderWeeklyGovernance()` function to the section render
- Marking meeting complete triggers XP + weekly streak (amount TBD in progression design session)

## Sound Library
- Full interaction → sound mapping to be created as a written spec first
- Every interaction gets a unique sound character:
  - Save, Delete, Section complete, Level up, Tab switch, Meeting done, Suggestion sent, AI summary generated, and more
- Implementation follows after spec is locked

## UI Polish (list to be created)
- Sidebar section reorganization
- Dashboard card glow effect when a section reaches 100% completion
- Mobile sidebar collapse (hamburger menu)
- Additional polish items TBD from dedicated planning session

## Font & Style Panel
- Gear icon opens panel
- Curated font pairings (not full Google Fonts catalog)
- Size scale: S / M / L
- Corner-radius / softness slider for panel edges

## 3-Band EQ in Media Player
- Bass / Mid / Treble sliders
- Applied to Web Audio output

## Make Suggestion Feature
- Button top-right of dashboard
- Opens a floating text file for Veronica to write her suggestion
- Syncs to cloud so Daniel can see it
- Suggestions persist visually on dashboard
- File + lightbulb icon at bottom-left of dashboard shows suggestion history

## AI Weekly Governance Summarizer
- Bot icon in Weekly Governance tab header
- Scans that week's user-entered fields only (scoped to that tab)
- Generates a bullet-point summary
- Brief confirmation popup on completion
- Summary stored in "Previous Summaries" archive
- Previous summaries accessible via icon in the same header row
- Bot sees only current week's inputs; cannot access other sections

## Export (Scope TBD — Prototype 3)
- Format and scope to be discussed before Prototype 3 begins
