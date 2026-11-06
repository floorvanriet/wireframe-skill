---
name: wireframe
description: Create mid-fi wireframes as a self-contained HTML/CSS file from a screen or flow described in words. Use this skill for requests like "make a wireframe of...", "sketch the structure of...", "show me what X would look like", "wireframe for...", "make a lo-fi or mid-fi design of...", or whenever someone describes a screen or flow and wants to see it. Also triggers on "screen layout", "page layout", "interface sketch", "UI sketch", "concept site" or wireframes for several parts of a product, in any language. Use it proactively too when a user describes a UX problem and visual structure would help clarify the solution.
---

# Wireframe

Create mid-fi wireframes as a single self-contained HTML file. Multiple screens side by side, responsive, grayscale with one accent color, real copy.

---

## Core principles

**Mid-fi means:**
- A grayscale palette (see tokens below), plus one accent color (`--accent`) for primary actions and active states. That makes the main action visible at a glance; no other color goes in.
- Real labels, titles and headings, no "Lorem ipsum". Write the copy in the language the product's end users will see; if that isn't clear, use the language of the request. That way the wireframe can be shown to stakeholders as is, even when the conversation happens in another language.
- Placeholder blocks for images (no real assets)
- Lucide line icons where an icon carries meaning (see Icons)
- Hover states on everything clickable (see Hover states)
- A clear typographic hierarchy
- No decoration, no shadows, only subtle borders

**Never:**
- Brand colors, or any color besides the accent
- Real images, photos, logos or illustrations
- Emoji or text symbols as icons (☰, ×, ›): use Lucide
- Animations (a short `transition` on hover is fine)
- Explanations inside the wireframe itself (annotations go outside it)

---

## Support the creative process

A wireframe is a thinking tool: it helps the user get clear on *what* and *why* by reasoning out loud, doubting and iterating. Your job is to support that process, not to take it over. That cuts both ways: don't just build without any discussion, and don't bury the user in talk before anything appears on the canvas. The screen is a conversation piece, not a deliverable.

### Per kind of input

- **New request:** open your reply with a short sparring block: the 2-3 choices that matter most, each with its options and your preference with a reason. Include interaction, not just layout: what happens on tap or click, where feedback appears, what can be undone, modal or separate page, inline or an extra step. Then build your preferred option, so there's something concrete to react to. A few bullets, not an essay. (Vague request with a complex scope? Ask the one question from Optimization intent first.)
- **Exploratory request** ("I'm torn between...", "what would work for...", thinking out loud): spar only. Lay out the options with their trade-offs and your preference, then ask whether to build one of them, and which.
- **Follow-up input:** respond on substance first: think along, add to it, expose a weakness or an alternative. Change the wireframe only once something has been decided, not with every passing thought. Not sure whether it's sparring or deciding? Ask briefly: "Shall I apply this, or think it through first?"

### How to spar

- **Push back out loud.** If a pattern might not work in this context (e.g. a shortlist when there are only 2 items), say so instead of building it blindly.
- **Offer directions, not done deals.** When a choice is genuinely open, show A and B side by side in the wireframe rather than only describing them, and say which you prefer.
- **Iterate in small steps.** Expect changes per element. Build on what the user selects or points at.
- **Don't force a decision.** The goal is clarity; the choice can come later.
- **Keep it light.** One line per option, a handful of bullets in total, and at most one focused question. The wireframe speaks for itself, so don't walk through what's in it; only mention what the user can't see, like an assumption or what happens on click.

---

## UX principles

- **Question the concept, not just the layout.** Keep checking whether the underlying function actually holds up, and challenge it, not only "what does it look like".
- **Don't claim a status the system can't know.** Base the UI on available data. If something can't be known, show the action instead of a status, or let the user mark it themselves.
- **Match content fidelity to the purpose of the screen.** If the point is structure or navigation, make the content low-fi (placeholder lines) so the focus stays on the subject.
- **Wireframe the key states side by side.** Logged in/out, empty/filled, open/closed: that makes the real decisions visible.
- **Translate navigation deliberately to smaller screens.** Keep one persistent anchor so the transition doesn't jar; prioritize and group instead of showing everything. One navigation structure, several shells, one source.

---

## Delivery

- **Keep each wireframe one self-contained HTML file.** No separate JS/CSS files next to it: previews often render the file standalone, without sibling files. The two CDN links in the base template (IBM Plex Sans via Google Fonts, Lucide via jsDelivr) are the exception; those load fine in previews. Want reuse? Inline a master template and sync the copies.
- **For a large set of screens, add a fixed screen switcher** (e.g. a dropdown) to jump between them.
- **For a concept that spans several product parts, build a concept site** (see below).

---

## Concept site

When a concept covers several parts of a product (onboarding, search, account...) and the user wants to show or review it as a whole, build a concept site: one page per part, connected by the same menu bar. Stakeholders get one place to walk through the whole concept, and you can iterate on one part without touching the rest.

- **Menu bar** at the top of every page, on the canvas, above the frames. Left: the concept name with an `info` icon whose tooltip holds the version, date and a one-line explanation. Then a divider, then one link per part. The current page gets `aria-current="page"` and is styled `--text-primary`/600; the rest `--text-secondary`. When the links don't fit, the bar scrolls horizontally rather than wrapping. For a large concept (more than about 15 screens), add a "Go to screen" dropdown at the right end of the bar that jumps to any screen on any page; for smaller concepts the menu is enough.
- **IA first.** The first link is an IA page: the structure of the product with a link to every part. It's also the entry page.
- **Each part page** is a normal wireframe: frames side by side, frame labels, the dotted canvas.
- **Separate files when they'll be opened together.** If you can write a folder that the user opens in a browser or hosts (working locally, in a repo), make `index.html` for the IA plus one file per part with a short slug (`onboarding.html`), linked relatively.
- **One file when it will be previewed on its own.** A single artifact or chat preview renders one file standalone, so links to other files break there. Put all parts in one file as sections, switched by the menu via `#hash` links (`#onboarding`).
- **Keep the menu identical everywhere.** Inline it in every file from one master copy, so each page still works on its own. When a part is added, renamed or removed, update the menu in every file in the same go.

---

## Design tokens

```css
:root {
  --bg:        #F5F5F5;   /* page background */
  --surface:   #FFFFFF;   /* cards, panels */
  --border:    #D1D1D1;   /* borders */
  --muted:     #E8E8E8;   /* placeholder blocks */
  --text-primary:   #1A1A1A;
  --text-secondary: #595959;   /* meta, placeholders, labels in image blocks */
  --text-disabled:  #AAAAAA;   /* disabled controls only */
  --accent:       #1560D0;   /* the only color: primary actions, active states */
  --accent-hover: #1250B0;
  --hover-bg:     #F0F0F0;   /* hover on light or transparent elements */
  --border-hover: #AAAAAA;   /* hover on bordered elements */
  --font: 'IBM Plex Sans', system-ui, sans-serif;
}
```

These tokens are tuned for WCAG AA (4.5:1): `--text-primary` and `--text-secondary` pass on every surface color here (`--surface`, `--bg`, `--hover-bg`, `--muted`, `--border`); `--accent` as text passes on all of them except `--border`; white passes on `--accent`. Accessibility starts in the wireframe, so keep it that way: don't add lighter greys for text. The one exception is `--text-disabled` (2.3:1): use it only for disabled controls, which WCAG exempts, never for readable text such as metadata.

---

## HTML structure

### Base template

Set `lang` to the language of the copy.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Wireframe: [subject]</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link href="https://fonts.googleapis.com/css2?family=IBM+Plex+Sans:wght@400;500;600&display=swap" rel="stylesheet">
  <style>
    /* tokens */
    *, *::before, *::after { box-sizing: border-box; }
    body { margin: 0; -webkit-font-smoothing: antialiased; }
    button, input, select, textarea { font: inherit; }  /* form controls don't inherit the font by default */
    /* layout + components */
  </style>
</head>
<body>
  <div class="wireframe-canvas">
    <div class="frame-row">
      <!-- frames here -->
    </div>
  </div>
  <script src="https://cdn.jsdelivr.net/npm/lucide@1/dist/umd/lucide.min.js"></script>
  <script>lucide.createIcons();</script>
</body>
</html>
```

### Layout for multiple frames

This canvas is what makes the output read as a wireframe at a glance, so use it as is.

```css
.wireframe-canvas {
  background-color: var(--bg);
  background-image: radial-gradient(circle, #C8C8C8 1px, transparent 1px);
  background-size: 20px 20px;
  padding: 40px;
  min-height: 100vh;
  font-family: var(--font);
}

.frame-row {
  display: flex;
  gap: 32px;
  align-items: flex-start;
  flex-wrap: wrap;
}

.frame {
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: 8px;
  overflow: hidden;
  flex-shrink: 0;
}

/* Width per device */
.frame.mobile  { width: 375px; }
.frame.tablet  { width: 768px; }
.frame.desktop { width: 1280px; }
.frame.auto    { width: 100%; max-width: 1280px; }
```

### Frame label (above each screen)

```html
<div class="frame-label">Screen 1: [name]</div>
<div class="frame mobile">
  <!-- content -->
</div>
```

```css
.frame-label {
  font-size: 11px;
  font-weight: 600;
  letter-spacing: 0.08em;
  text-transform: uppercase;
  color: var(--text-secondary);
  margin-bottom: 8px;
}
```

---

## Components

Write the HTML and CSS for components yourself, but stick to these values so wireframes look consistent across sessions. Give buttons and inputs a `min-height` with `inline-flex` centering rather than relying on padding: padding alone ends up just under 40px, and 40px is the minimum click target.

| Component | Spec |
|---|---|
| Primary button | `--accent` fill, white text, 14px/600, `min-height: 40px`, padding 0 20px, radius 6px |
| Secondary button | Transparent, `--accent` text, 1.5px `--accent` border, otherwise as primary |
| Text button / inline action | "Edit", "Set status", "Change": `--accent` text, 14px/500, no border. Still a 40px target: `min-height: 40px` with `inline-flex`, or padding plus an equal negative margin when it sits inside a line |
| Input | Label above (13px/500, `--text-primary`, 4px gap). Field: 1px `--border`, radius 6px, `min-height: 40px`, padding 0 12px, 14px, placeholder text in `--text-secondary` |
| Image placeholder | `--muted` block with a fixed `aspect-ratio`, centered label in `--text-secondary` 13px naming content and ratio ("Product photo 16:9") |
| Card | `--surface`, 1px `--border`, radius 8px, `overflow: hidden`. Body padding 16px, gap 4px: overline 11px uppercase `--text-secondary`, title 15px/600, meta 12px `--text-secondary` |
| Tag | 12px/500, padding 2px 8px, radius 4px (smaller than its card), `--muted` background, `--text-secondary` text |
| Mobile nav bar | Padding 12px 16px, bottom border. Logo text 16px/600 left, Lucide `menu` in a 40×40 button right, with `aria-label` |
| Desktop nav bar | Padding 16px 32px, bottom border. Logo, links (14px, `--text-secondary`, gap 24px, active `--text-primary`/500), primary button right |
| Stepper | 28px circles with 13px/600 numbers, 32px connecting line in `--border`. To do: `--muted`/`--text-secondary`. Active: `--accent`/white. Done: `--border`/`--text-secondary` |

Need a component that isn't listed? Derive it from these values (same radii, type scale and states) rather than inventing new ones.

---

## Optimization intent

If the request contains a direction ("fewer steps", "easier to scan", "less busy", "quicker to understand"), use it as a lens: choose components, hierarchy and copy structure that reinforce that direction.

If the request is vague *and* the scope is complex (3+ screens or a flow), ask one focused question: "What do you want to improve: overview, speed, trust, or something else?"

Don't ask for single screens or when the intent is already clear.

---

## Approach per input type

### Screen or flow described in words

1. Identify the screens in the description (each screen = one frame)
2. Determine the device type (mobile for apps when not stated, desktop for web)
3. Put all frames in one file, side by side
4. Use real copy that fits the context, in the end users' language (see Core principles)

### Number of frames

- 1 screen: show at device width
- 2-4 screens: side by side in one row
- 5+ screens: two rows, or scroll horizontally

---

## Hover states

Always add them. Wireframes are meant to be clickable, and hover shows what's interactive. There are three patterns. Apply them to the classes you create in *this* wireframe, not to a fixed list:

```css
/* 1. Accent-filled: primary button, active chip or tab, FAB */
.btn-primary:hover   { background: var(--accent-hover); cursor: pointer; }

/* 2. Light or transparent: secondary button, icon button, list item */
.btn-secondary:hover,
.nav-menu:hover      { background: var(--hover-bg); cursor: pointer; }

/* 3. Bordered: clickable card, chip, choice option */
.card:hover          { border-color: var(--border-hover); cursor: pointer; }
```

Every interactive element gets `cursor: pointer`. Non-interactive elements (text, labels, placeholders, cards that don't link anywhere) get no hover.

---

## Icons

Use **Lucide** via CDN: it works in previews and in external browsers. The base template already loads it, pinned to major version 1 so a future release with renamed icons doesn't silently break existing wireframes.

Use icons like this:

```html
<i data-lucide="chevron-left" aria-hidden="true"></i>
```

Set the size in CSS:

```css
[data-lucide] { width: 16px; height: 16px; vertical-align: -2px; stroke-width: 1.75; }
```

Adjust `width`/`height` per context:
- Inline in text: 16×16px
- Standalone (button, nav): 20×20px
- Large decorative: 24×24px max

Color inherits from the parent via `stroke: currentColor`, so no separate color is needed.

Accessibility: decorative icons get `aria-hidden="true"`. Icons without a visible label get a parent with `aria-label`.

**Names that work** (checked against Lucide 1.x). An unknown name throws no error, it just renders nothing. If you're unsure about an icon that isn't listed, pick the closest one from this list.

- **Navigation:** back `chevron-left`, forward `chevron-right`, up/down `chevron-up` / `chevron-down`, arrows `arrow-left` / `arrow-right` / `arrow-up` / `arrow-down`, home `home`, menu `menu`, external link `external-link`
- **Actions:** add `plus`, delete `trash-2`, edit `pencil`, save `save`, copy `copy`, paste `clipboard`, refresh `refresh-cw`, undo/redo `undo-2` / `redo-2`, download `download`, upload `upload`, share `share-2`, search `search`, filter `filter`, sort `arrow-up-down`, close `x`, confirm `check`
- **Status and feedback:** info `info`, warning `alert-circle`, error `x-circle`, success `check-circle`, loading `loader`, locked/unlocked `lock` / `lock-open`, visible/hidden `eye` / `eye-off`
- **Content and media:** file `file`, folder `folder`, image `image`, attachment `paperclip`, link `link`, document `file-text`, list `list`, table `table`, chart `line-chart` / `bar-chart-2`, tag `tag`
- **People and communication:** user(s) `user` / `users`, message `message-circle`, email `mail`, notification `bell`, settings `settings`, adjust `sliders-horizontal`, calendar `calendar`, clock `clock`, favorite `star`

---

## Finishing touches

Small details that make wireframes feel modern without going high-fidelity.

**Typography:**
- `text-wrap: balance` on all headings (h1, h2, section titles)
- `font-variant-numeric: tabular-nums` on numbers that sit side by side or update (amounts, times, counters, measurements)
- Labels above input fields: always `font-weight: 500`, never regular
- Metadata and timestamps: consistently `font-size: 12px`, color `--text-secondary`. Size and position set them apart, not a lighter grey

**Space and alignment:**
- Concentric border radius: a nested element always has a smaller radius than its parent. Card (8px) → tag inside it (4–5px), not 8px as well
- Vertical whitespace between sections: use fixed steps (16 / 20 / 24 / 32px), no arbitrary values
- Section labels (uppercase, small, spaced): always `letter-spacing: 0.08em`, `font-size: 10–11px`

**Interactive elements:**
- Minimum click target of 40×40px on buttons and chips, even when the visual size is smaller. This includes text-only buttons and inline actions ("Edit", "Set status"): give them `min-height: 40px` with `inline-flex`, or grow the hit area with padding plus an equal negative margin so the layout doesn't shift
- `transition: border-color 0.12s` on cards and inputs that have a hover, not `transition: all`

**Separators:**
- Use `border-bottom: 1px solid var(--border)` to separate sections, not extra whitespace alone
- Avoid double separation: not both a line and extra padding

---

## Quality checklist

Check before delivering:

- [ ] No color outside the grayscale tokens and `--accent` (only for primary actions and active states)
- [ ] Clickable elements have a hover state, static elements don't
- [ ] Icons via Lucide, no emoji or text symbols
- [ ] All readable text passes WCAG AA contrast: `--text-disabled` only on disabled controls
- [ ] Real labels and headings in the end users' language (no placeholder text like "Heading here")
- [ ] Every frame has a frame label
- [ ] Images are placeholder blocks with a ratio and a label
- [ ] Typographic hierarchy is visible (h1 > h2 > body > meta)
- [ ] Responsive: frames scale correctly on smaller screens
- [ ] Concentric border radius: nested elements have a smaller radius than their parent
- [ ] Numbers use `tabular-nums`
- [ ] Section labels: uppercase, 10–11px, `letter-spacing: 0.08em`
- [ ] Vertical spacing in fixed steps (16 / 20 / 24 / 32px)
- [ ] Buttons, inputs and chips are at least 40px high or have a 40×40px click target
- [ ] Separators consistent, no double separation
