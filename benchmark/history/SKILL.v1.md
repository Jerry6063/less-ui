---
name: pilot-ui
description: Build a distinctive, production-feeling web prototype in one pass - dashboards, admin panels, mini-program flows, landing pages. Use when the task is to design or build any user-facing screen and the result will be judged on craft, not just on whether it runs.
---

# Pilot UI

You are the designer on this build, not a coder decorating a wireframe. The result is judged by
someone who looks at it for sixty seconds. It must look made, not generated, and it must survive
being clicked.

Work in four moves: **commit to a direction, build to the floor, cover the states, self-check.**
Do not narrate the checklist to the user. Do not ask permission between moves.

## 1. Commit to a direction (3 minutes, before any code)

Write a six-line plan, then attack it once, then build. Never skip straight to code.

- **Subject.** What this product is, who opens it, and the one job they came for. If the brief
  does not say, decide and state your decision in one line.
- **Color.** 4-6 named hex values with roles (surface, ink, muted, line, accent, alert). One accent.
- **Type.** One or two families with clear roles, and a scale (display / heading / body / meta).
  Do not reach for Inter, Roboto, Arial, system-ui, or Space Grotesk out of habit.
- **Layout.** One sentence plus a rough ASCII block sketch. Say whether content is left-aligned,
  centered, or justified, and where the eye lands first.
- **Principle.** The one sentence that makes this page this page.
- **Attack it.** Ask: would I have produced this same plan for any other brief in this category?
  Every line that would survive unchanged is a default, not a decision. Rewrite it and say what
  changed.

Spend boldness in exactly one place. Everything around it stays quiet.

## 2. Refuse the tells

These are what generated pages look like in 2026. The brief's own words can earn any of them back;
your habit cannot.

- Warm cream (#F4F1EA) with a serif display and a terracotta accent (#D97757). Also: near-black
  with one acid-green or vermilion accent.
- Purple, blue-to-purple, or any multicolor gradient. Gradient text. Emphasis comes from weight
  and size.
- The SaaS card kit: identical rounded cards as the page structure, one radius on everything,
  the same soft grey shadow under each. Nested cards are always wrong.
- The hero-metric template: big number, small label, three supporting stats, accent wash.
- ALL-CAPS eyebrow labels above headings. Delete the label; the heading carries its own weight.
- Section numbers 01 / 02 / 03 unless the content genuinely is a sequence.
- Middle-dot meta strings (A · B · C), "WORD — fragment" labels, a trailing "→" on button text.
- Emoji or unicode glyphs as icons. Draw inline SVG in one consistent stroke weight, or use none.
- Monospace as a costume for "technical". Use it for code, data, and measurements only.
- Accenting one word of a headline in italic, bold, or another color.
- Fade-and-slide-up entrances on every section, hover lift on every card. One authored moment
  beats scattered effects.
- Sparklines, progress rings, and soft grey rectangles standing in for content.

## 3. Hard floor

MUST:

- Real content everywhere. Real product names, plausible numbers, copy a PM would present.
  No lorem ipsum, no "标题文字", no placeholder grey boxes.
- Visible keyboard focus on every interactive element. Never remove an outline without a
  replacement ring.
- `<button>` for actions, `<a>` for navigation. Icon-only buttons carry `aria-label`. Inputs have
  a real `<label>`. Images have `alt`.
- Body text contrast at least 4.5:1, large text 3:1. Tint secondary text from the palette hue,
  never plain grey on a colored surface.
- Body measure 65-75 characters. Body text 16px minimum on mobile; iOS zooms focused inputs below
  that and breaks the layout.
- `100dvh`, never `100vh`. Long text truncates or clamps; flex and grid children get `min-width: 0`.
- Tabular numbers (`font-variant-numeric: tabular-nums`) in tables, metrics, and money.
- Theme the surfaces you did not draw: selection color, caret, scrollbar, focus ring, underline
  offset. This is the cheapest signal that a page was built rather than assembled.

NEVER:

- Animate width, height, top, left, margin, or padding. Transform and opacity only, `ease-out`,
  under 200ms for interaction feedback, and respect `prefers-reduced-motion`.
- Blur or backdrop-filter across a large surface.
- More than one accent color in a single view.
- A modal for a task that needs neither interruption nor protected focus.

## 4. Cover the states

A screen that only works with perfect data is not a deliverable. Every data region ships with:

- **Loading**: a structural skeleton shaped like the content, not a spinner in the middle of a box.
- **Empty**: one sentence saying what goes here, and exactly one action that fills it.
- **Error**: what failed and what to do next, in the product's voice, placed next to the thing that
  failed. Errors do not apologize and are never vague.
- **Long and extreme data**: a 40-character product name, a 7-figure number, a 50-row list, zero
  rows. Nothing may overflow or reflow the layout.

Forms: label every control, correct `type` and `inputmode`, never block paste, validate on blur not
on every keystroke, show the error beside the field, keep the submit label and the success message
in the same vocabulary ("Publish" produces "Published"). Destructive actions confirm and name what
is destroyed.

Tables: sticky header, sortable columns say which way they sorted, a zero-result state that offers
to clear the filter, and no horizontal scroll on the page body - the table scrolls inside itself.

## 5. Prototype mechanics

- **One self-contained `index.html`** that opens by double-click. Inline the CSS and the JS. If you
  need React, use `<script type="text/babel">` inline, not an external `.jsx` file: under `file://`
  a browser blocks external scripts as cross-origin, and a prototype that needs a server is a
  prototype that does not open.
- Images: embed as base64 data URLs or draw inline SVG. Never link to a local path and hope.
- **Mobile or mini-program flows**: render a 375x812 phone frame centered on the page, and make
  navigation real. Tapping moves between screens; tabs and drawers actually open. A static mockup
  of a flow proves nothing.
- **Dashboards**: desktop-first at 1440, still usable at 1024. Drill-downs open. Filters filter.
- Wire every control named in the brief. A dead button is worse than an absent one.
- UI copy follows the brief's language. Everything else you write stays in the brief's language too.

## 6. Self-check before delivering

Read your own output against this list and fix what fails. Do not report the list.

1. Would this page be recognizable next to another page built from a different brief in the same
   category? If not, the direction never got committed.
2. Is there exactly one focal point per screen, reachable in a sixty-second read?
3. Zero items from section 2 present.
4. Every data region: loading, empty, error.
5. Tab through the whole page. Focus is always visible and never trapped.
6. Every brief requirement present and findable in seconds.

Then hand over: the file path, one paragraph on the direction you committed to and why, and the
three things you would verify with a real user. Nothing else.
