# Pim Minderman Portfolio — Design System

This is the lightweight visual and interaction system used by the portfolio. The implementation in `index.html` is the source of truth; this guide makes it easier to extend consistently.

## Foundations

### Colour

| Token | Light | Dark | Use |
| --- | --- | --- | --- |
| `--bg` | `#F8FAFC` | `#0F172A` | Page background |
| `--ink` | `#171717` | `#F8FAFC` | Primary text |
| `--muted` | `#64748B` | `#CBD5E1` | Supporting text |
| `--line` | `#DBE2EA` | `#475569` | Dividers and outlines |
| `--card` | `#FFFFFF` | `#111827` | Snapshots and raised surfaces |

Interactive focus uses a 2px teal outline (`#0F766E` in light mode and `#5EEAD4` in dark mode), offset by 3px.

### Typography

Font family: **Inter** with system sans-serif fallbacks. Use weights 400, 500 and 600 only.

| Style | Size / line-height | Weight | Use |
| --- | --- | --- | --- |
| Intro | 20px / 1.5 | 400 | Personal introduction |
| Story title | 20px / 1.25 | 500 | Desktop case-study title |
| Story title, mobile | 16px / 1.25 | 500 | Mobile case-study title |
| Body | 14px / 1.6 | 400 | Story summaries and supporting copy |
| Company | 16px | 400 | Desktop company name |
| Company, mobile | 14px | 400 | Mobile company name |
| Labels | 12px | 600 | Snapshot labels and buttons |
| Eyebrows | 14px | 600 | Uppercase section labels |
| Footer copyright | 12px | 400 | Secondary footer text |

Headings use `letter-spacing: -0.025em`; uppercase labels use `0.06–0.08em` letter spacing.

### Spacing and layout

Use a 4px-based rhythm where possible: `4, 8, 12, 16, 24, 32, 48, 64`.

- Content rail: `min(1060px, 100% - 64px)` on desktop; 32px total side gutter on mobile.
- Intro rail: maximum 720px, centred.
- Desktop story grid: 170px company column, 50px gap, flexible story column.
- Breakpoint: 600px. Stories become a vertical flow: title and copy, snapshot button, then company.
- Story rows: 34px vertical / 30px horizontal padding on desktop; 28px vertical / no added horizontal padding on mobile.

## Components

### Portrait

- Circular photograph: 128px desktop, 108px mobile.
- One 1px border plus an outer 1px outline with a 5px gap.
- Gentle vertical float: 4 seconds, ease-in-out, 5px maximum travel.

### Experience pill

Used for previous-company links.

- 14px text; 7px × 10px padding.
- Full pill radius (`999px`).
- 1px `--line` border and a low-contrast white surface.
- Hover increases border and text contrast; do not use heavy fills or shadows.

### Story row

Each case study contains a company label, title, short summary and **View snapshot** trigger.

- Company logo: circular, 24px desktop / 20px mobile.
- Divider: 1px `--line` above the first row and below every row.
- Keep one primary story idea in the title and a short, outcome-focused summary below it.

### Snapshot trigger

- Label: 12px, weight 500.
- Padding: 5px × 8px; full pill radius.
- Sits 12px below the story copy.
- The trigger must work with mouse, keyboard and touch. Do not make hover the only way to open a snapshot.

### Snapshot panel

- Maximum width: 720px, with a 16px viewport gutter.
- Maximum height: viewport height minus 32px; panel scrolls internally when needed.
- 8px outer padding, 12px rounded corners and a restrained raised shadow.
- Media: 16:9, 7px radius.
- Content labels: 12px uppercase, followed by 14px body copy with 6px separation.
- Close control: circular 28px button at the top-right.

On larger screens the snapshot opens on hover and stays open while moving between the trigger and panel; it also opens on click. On smaller screens it opens in the story flow. The viewport-positioning logic chooses the available space above or below the trigger.

### Theme control

- Borderless black-and-white diagonal circle.
- 20px desktop; 16px mobile.
- Fixed top-right: 20px desktop / 12px mobile.
- The visual change is supplemented by an accessible label and pressed state. The selected theme is saved locally in the browser.

### Footer

- Top divider and compact 12px copyright line.
- Contact uses the only external-arrow treatment; other external links remain text-only.

## Motion

Motion is quiet and decorative, not required to understand or use the portfolio.

- Portrait float: 4 seconds, infinite.
- Snapshot-media shine: 5.5 seconds, infinite.
- Hover and panel transitions: 150–200ms.
- Honour `prefers-reduced-motion: reduce` by effectively disabling animation and transition timing.

## Accessibility rules

- Keep visible keyboard focus for all links and buttons.
- Use descriptive alternative text for meaningful images; company logos are decorative when their name is already adjacent.
- Mark snapshots as dialogs and connect each trigger with `aria-controls` and `aria-expanded`.
- Support Escape to close an open snapshot and clicking or tapping outside it to dismiss it.
- Preserve strong light and dark colour contrast when adding colours or surfaces. Test any new foreground/background pairing before publishing.

## Social share card

The document includes Open Graph and Twitter metadata. Keep these aligned when changing the portfolio identity:

- Title: `Pim Minderman — Product Designer`
- Description: short, plain-language portfolio summary
- Image: an absolute public URL, with useful alt text
- Canonical URL: the live GitHub Pages address

## Extension checklist

When adding a story or component:

1. Reuse the typography, colour and spacing rules above.
2. Check desktop, mobile and dark mode.
3. Verify keyboard focus, click/tap use and reduced-motion behaviour.
4. Keep the page lightweight: use local media assets and avoid adding frameworks for a single component.
