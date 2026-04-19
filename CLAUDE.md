# Swoosh — Claude Code Project Rules

## Design System (Linear / Stripe / Vercel lineage)

Apply to every CSS, HTML, and UI change. Precedence when rules conflict:
**Accessibility → Hierarchy → Spacing → Depth → Color → Motion**

---

### Core principles

1. Strip everything that doesn't serve the user's task, then add just enough warmth so it feels alive.
2. Hierarchy through weight, size, and color — never through borders or boxes.
3. One job per element. A banner either announces or prompts action, not both at equal weight.
4. Accent color is for the *one* thing you want clicked. Everything else is neutral.
5. All spacing, sizing, and radii come from the systems below. No arbitrary numbers.
6. Prefer real `border` + real `box-shadow`. Avoid sub-pixel tricks — they fail at 1× zoom and in dark mode.

---

### Color tokens

Token names used in this project (never hard-code colors outside the token layer):

```
--ink              primary text
--paper            page background
--warm-gray        borders, dividers
--muted            secondary text, labels
--card-bg          raised card surface
--surface-raised   chips/pills that sit ON cards or banners
--accent-amber     primary accent (rename to --accent in new work)
--accent-amber-rgb RGB triplet for rgba() use
--accent-sage      secondary / success-adjacent
--accent-rose      danger / destructive
--status-active    green
--status-cooling   amber
--status-abandoned red
--category-work    blue  (#4a7ab5)
--category-social  green (#4a9a5a)
--category-dev     purple (#8a6ab5)
--category-media   rose  (#b55a6a)
--category-ai      amber (#b5823a)
--category-jio     blue  (#3535f3)
```

Depth tokens already defined in `:root`:
`--banner-shadow`, `--banner-highlight`, `--btn-shadow`, `--btn-shadow-hover`, `--focus-ring`, `--card-shadow`, `--card-shadow-hover`, `--ease-snappy`, `--dur-fast`, `--dur-base`

Dark-mode overrides live in `.theme-dark` and `@media (prefers-color-scheme: dark)`. Never write dark styles outside those scopes.

---

### Spacing — 4/8px grid (strict)

Only: `4, 8, 12, 16, 20, 24, 32, 40, 48, 64, 80, 96`

| Use case | Value |
|---|---|
| Icon-to-text gap | `8px` |
| Inline element gap | `8–12px` |
| Button padding (vertical / horizontal) | `9px / 16px` → height `34px` |
| Card padding | `20–24px` |
| Banner padding | `16px 20px` |
| Section vertical rhythm | `24–32px` |
| Page gutter | `32–48px` |

**Never use** `3, 5, 7, 10, 14, 18, 22px`.

---

### Radii — monotonic (smaller as elements nest deeper)

| Element | Radius |
|---|---|
| Card, banner, panel | `12px` |
| Button, input, chip | `8px` |
| Small tag, inline dot | `6px` |
| Count pill / badge | `999px` |
| Avatar | `50%` |

**Forbidden:** `10px`, `14px`, `20px`, `24px` radii. Pill-shape (`999px`) only for count badges, never buttons.

---

### Typography

```
Font body:  'DM Sans', sans-serif
Font serif: 'Newsreader', serif  (editorial headings only)
```

| Role | Size / weight |
|---|---|
| Display H1 | 28–32px / 300 |
| Section H2 | 18px / 400 italic (Newsreader) |
| Card title | 15px / 600 / -0.2px |
| Body | 14–15px / 400 |
| Secondary | 13px / 400 / `--muted` |
| Label / caps | 10–11px / 500 / uppercase / +0.5–1.5px tracking |
| Button | 12px / 600 |
| Count badge | 11px / 700 |

---

### Shadows & depth

Every raised surface uses two layers:
```css
box-shadow:
  0 1px 2px rgba(26, 22, 19, 0.04),
  0 6px 18px rgba(var(--accent-amber-rgb), 0.07),
  inset 0 1px 0 rgba(255, 255, 255, 0.7);
```

Use `--card-shadow` for cards, `--banner-shadow` for banners, `--btn-shadow` for primary buttons. Never pure-black shadows in light mode.

Corner glow (`::before` radial-gradient) is for T3 banners and hero surfaces only — never on routine/recurring elements.

---

### Banner tiers

Default to **T1**. Escalate only when the criteria are met.

| Tier | Frequency | Treatment |
|---|---|---|
| T1 — Routine | Every session | Neutral — looks like a sibling of cards. No glow. |
| T2 — Action required | Occasional | Accent border + soft shadow. No corner glow. |
| T3 — Critical / one-time | Rare | Full kit: tinted fill + border + corner glow + two-layer colored shadow. `role="alert"`. |

Rule: if you see a banner multiple times per session, it's T1 — no exceptions.
Max 2 accent-saturated elements per banner (count badge + primary CTA). Everything else neutral.

---

### Motion

- Default: `150–200ms ease` or `cubic-bezier(0.16, 1, 0.3, 1)` for snappy ease-out (`--ease-snappy`)
- Hover: `translateY(-1px)` + shadow upgrade. Never `scale > 1.01`.
- Mount: `fadeUp` — fade + `8–12px translateY`, `300–400ms`.
- **Never `transition: all`** — list exact properties: `box-shadow, transform, background, border-color, color`
- Always include `@media (prefers-reduced-motion: reduce)` with `0.01ms` durations.

---

### Accessibility (non-negotiable)

- Every interactive element must have `:focus-visible` using `--focus-ring`.
- Minimum touch target: 34×34px.
- Decorative icons: `aria-hidden="true"`.
- Status banners: `role="status"` + `aria-live="polite"`. Alerts: `role="alert"` + `aria-live="assertive"`.
- Color alone must never carry meaning — pair with icon, label, or weight.

---

### Common mistakes — don't do these

| Don't | Do |
|---|---|
| Hard-code hex colors in CSS | Use tokens from `:root` |
| Pill-shaped buttons (`border-radius: 999px`) | `8px` radius buttons |
| Second filled button next to primary | Primary filled, secondary ghost |
| Solid accent count badges (white text) | `rgba(accent, 0.1)` bg + accent text |
| `transition: all` | List exact properties |
| Arbitrary spacing (7px, 13px, 17px) | 4/8px grid only |
| Corner glow on routine banners | Glow only for T3/hero surfaces |
| 4+ accent-saturated elements in one banner | Max 2: badge + CTA |
| `border-radius: 50%` on non-avatar icons | `8px` rounded-square container |

---

### Reference products (in order of precedence)

1. **Linear** — depth, glow, dark mode, typography
2. **Stripe** — shadows, form fields, button states
3. **Vercel** — neutrality, spacing rhythm
4. **Raycast / Arc** — menus, hotkeys, inline UI
