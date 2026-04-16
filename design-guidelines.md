# Autoscuola Rampone — Student App Design Guidelines

## Overview

Mobile app for driving school students. Tracks lesson hours, logs sessions, manages bookings, shows profile. Clean and minimal. Target: 18–25 year olds.

---

## Brand Colors

| Role | Hex | Usage |
|---|---|---|
| Primary accent | `#f39200` | Buttons, progress bar, CTAs |
| Dark base | `#2a303c` | Headers, nav bar, primary text |
| Background | `#ffffff` | Screen backgrounds |
| Surface | `#f3f3f3` | Cards, input fields, secondary bg |
| Success | `#00d084` | Signed-off sessions, confirmations |
| Text primary | `#2a303c` | Body text |
| Text secondary | `#abb8c3` | Subtitles, timestamps, labels |

---

## Typography

- **Font:** System default (SF Pro on iOS, Roboto on Android) — no custom font for MVP
- **Hierarchy:**
  - H1: 28px bold — screen titles
  - H2: 20px semibold — section headers
  - Body: 16px regular
  - Caption: 13px regular — timestamps, labels
- **Alignment:** Left-aligned throughout. Center only for empty states.

---

## General Principles

- White backgrounds, no heavy gradients
- Cards use `#f3f3f3` background, 12px border radius, subtle shadow
- Orange (`#f39200`) reserved for primary actions only — one per screen
- Generous whitespace — do not crowd elements
- Icons: outline style (e.g. Phosphor or Lucide)
- No dark mode in MVP

---

## Navigation

Bottom tab bar, 3 tabs:

```
[ Home ]   [ Sessions ]   [ Profile ]
```

- Active tab: icon + label in `#f39200`
- Inactive: icon + label in `#abb8c3`
- Tab bar background: `#ffffff` with top border `#f3f3f3`

---

## Screens

### 1. Home

Hero: total hours progress bar.

```
─────────────────────────────────
  Hi, Marco 👋
  Patente B

  ┌──────────────────────────┐
  │  12h / 30h               │
  │  [████████░░░░░░░]  40%  │
  └──────────────────────────┘

  Breakdown
  ┌──────────┐ ┌──────────┐ ┌──────────┐
  │ Urban    │ │ Highway  │ │ Night    │
  │  8h      │ │  3h      │ │  1h      │
  └──────────┘ └──────────┘ └──────────┘

  Last session
  ┌──────────────────────────────────┐
  │ 14 Apr · 1h 30min · Enzo   ✅   │
  └──────────────────────────────────┘
─────────────────────────────────
```

- Progress bar fill color: `#f39200`
- Progress bar track: `#f3f3f3`
- Breakdown in 3 equal cards
- Last session card tappable → navigates to Sessions tab

---

### 2. Sessions

List of past sessions + booking CTA.

```
─────────────────────────────────
  Sessions

  [+ Book a lesson]   ← primary orange button, full width

  ─────────────────────────────
  📅 14 Apr 2026 · 1h 30min
     Enzo · Urban + Highway
     ✅ Signed off

  📅 10 Apr 2026 · 1h 00min
     Paola · Urban
     ✅ Signed off

  📅 07 Apr 2026 · 2h 00min
     Enzo · Highway + Night
     ✅ Signed off
  ─────────────────────────────
```

- `[+ Book a lesson]` button: `#f39200`, white text, full width, 14px border radius
- Each session = card with subtle shadow
- ✅ in `#00d084`
- Pending sign-off: show ⏳ in `#abb8c3`
- Tapping `[+ Book a lesson]` pushes Booking Screen (not a tab)

---

### 3. Booking Screen

Pushed from Sessions tab. Not a bottom tab.

```
─────────────────────────────────
  ← Back        Book a Lesson

  📅 Pick a date
  ┌──────────────────────────────┐
  │   < April 2026 >             │
  │  Mo Tu We Th Fr Sa Su        │
  │  ..  1   2  [3]  4   5   6  │
  │   7   8   9  10  11  12  13  │
  │  ...                         │
  └──────────────────────────────┘

  🕐 Available slots
  ┌──────┐ ┌──────┐ ┌──────┐ ┌──────┐
  │09:00 │ │10:30 │ │14:00 │ │15:30 │
  │  ✕   │ │  ✓   │ │  ✕   │ │  ✓   │
  └──────┘ └──────┘ └──────┘ └──────┘
  (taken = grayed out, not tappable)
  (free = tappable, orange on select)

  📝 Notes (optional)
  ┌──────────────────────────────┐
  │ e.g. prefer highway route    │
  └──────────────────────────────┘

  [Send Request]   ← primary orange button
─────────────────────────────────
```

- Selected date: circle fill `#f39200`
- Available slot selected: border `#f39200`, text `#f39200`
- Taken slot: background `#f3f3f3`, text `#abb8c3`, not tappable
- After `[Send Request]`: show confirmation toast "Request sent! School will confirm shortly."
- Instructor assigned by school after request — not shown to student at booking time

---

### 4. Profile

Read-only. Data set by admin.

```
─────────────────────────────────
  Profile

  ┌──────────────────────────────┐
  │  Marco Bianchi                │
  │  Patente B                    │
  └──────────────────────────────┘

  Personal
  ─────────────────────────────
  Date of birth      12/03/2005
  Email              marco@gmail.com
  Phone              +39 333 1234567

  Foglio Rosa
  ─────────────────────────────
  Issued             01/03/2026
  Expires            01/03/2027   ← red if <30 days left

  Instructor
  ─────────────────────────────
  Assigned           Enzo
─────────────────────────────────
```

- All fields read-only (no edit on student side)
- Foglio rosa expiry: turns `#cf2e2e` if within 30 days
- Clean label/value rows, no card borders needed — use whitespace separation

---

## Component Patterns

| Component | Spec |
|---|---|
| Primary button | `#f39200` bg, white text, 14px radius, 52px height, full width |
| Secondary button | `#f3f3f3` bg, `#2a303c` text, same radius |
| Card | `#f3f3f3` bg, 12px radius, shadow: 0 2px 8px rgba(0,0,0,0.06) |
| Input field | `#f3f3f3` bg, 10px radius, 16px padding, no visible border |
| Toast | Bottom of screen, `#2a303c` bg, white text, auto-dismiss 3s |
| Progress bar | Height 12px, track `#f3f3f3`, fill `#f39200`, 6px radius |
| Status badge ✅ | `#00d084` |
| Status badge ⏳ | `#abb8c3` |
| Expiry warning | `#cf2e2e` text only, no background |

---

## Spacing

- Screen horizontal padding: 20px
- Section gap: 24px
- Card inner padding: 16px
- Between list items: 12px

---

## Empty States

- Centered illustration (simple, line-style)
- Short message: "No sessions yet"
- Sub-text: "Your instructor will log your first lesson"
- No CTA needed on empty sessions (booking button already at top)
