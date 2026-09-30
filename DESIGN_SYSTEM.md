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
| Release source | 10px / 1.2 | 400 | Company and release type |
| Release title | 12px / 1.3 | 400 | Linked release title |
| Release description | 10px / 1.35 | 400 | One-line supporting summary |
| Eyebrows | 14px | 600 | Uppercase section labels |
| Footer copyright | 12px | 400 | Secondary footer text |

Headings use `letter-spacing: -0.025em`; uppercase labels use `0.06–0.08em` letter spacing.

### Spacing and layout

Use a 4px-based rhythm where possible: `4, 8, 12, 16, 24, 32, 48, 64`.

- Content rail: `min(1060px, 100% - 64px)` on desktop; 32px total side gutter on mobile.
- Intro rail: maximum 720px, centred.
- Desktop story grid: 128px company column, 24px gap, flexible story column.
- Breakpoint: 600px. Stories become a vertical flow: title and copy, snapshot button, then company.
- Story rows: 34px vertical / 30px horizontal padding on desktop; 28px vertical / no added horizontal padding on mobile.

The drawer changes the usable page width from the `md` breakpoint (768px) upwards. Any future compact-layout rules should respond to the page container width—not only viewport width—so titles do not become narrow when the drawer is open.

## Components

### Portrait

- Circular photograph: 128px desktop, 108px mobile.
- One 1px border plus an outer 1px outline with a 5px gap.
- Gentle vertical float: 4 seconds, ease-in-out, 5px maximum travel.

### Where I’ve worked

Previous-company links sit below Other projects as a four-column logo list.

- 28px circular logo and 16px company name on desktop.
- Two columns, 24px logos and 14px company names on mobile.
- Use a simple text underline on hover; keep the logo decorative when the adjacent company name is visible.

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

### Snapshot drawer

One persistent drawer displays the selected story; switching stories changes its content rather than opening another drawer.

- Mobile (below 768px): full-width overlay.
- From 768px: right-hand drawer reserves page space and shifts the page left.
- Width: `min(28rem, 48vw)` at 768px; 32rem at 1280px; 35rem at 1536px.
- Full viewport height, 24px inner padding, internal vertical scrolling and a left divider/shadow.
- Media: 16:9 with 7px corners.
- Detail rows: 12px uppercase label alongside 14px body copy.
- Close control: circular button at the top-right; Escape closes the drawer.
- Selecting another **View snapshot** keeps the drawer open and fades the content out/in over 140ms.

### Release card

Used at the bottom of a snapshot to link to relevant public releases or product updates.

- Section label: **Releases**.
- 2px-corner card with a 1px `--line` border, 8px internal padding and an inset 72px × 64px thumbnail (64px wide on mobile).
- Source line uses 10px regular Inter; it contains the company name and release type, without a logo.
- Title uses 12px regular Inter; supporting copy uses the full text column at 10px regular Inter and truncates with an ellipsis after one line.
- Use the release’s original image and full public title when available. Links open in a new tab without an additional arrow icon.

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
- Release-card hover: 150ms.
- Drawer entry/exit: 240ms; content switching: 140ms.
- Honour `prefers-reduced-motion: reduce` by effectively disabling animation and transition timing.

## Accessibility rules

- Keep visible keyboard focus for all links and buttons.
- Use descriptive alternative text for meaningful images; company logos are decorative when their name is already adjacent.
- Mark the persistent snapshot as a dialog and connect every trigger with `aria-controls="snapshot-drawer"` and `aria-expanded`.
- Support Escape and the visible close button. Do not claim outside-click dismissal unless it is implemented.
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
4. Keep the page lightweight: prefer local portfolio media; use the original public thumbnail only when linking to an external release.
