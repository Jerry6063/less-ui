# UI rules

Judge sees it for sixty seconds. Look made, not generated. Less is more professional.

1. Plan before CSS: the user and their one job; density follows that job; 4-6 hex colors with
   one accent; one or two typefaces, never Inter/Roboto/Arial/system-ui; a layout sketch; one
   principle. Attack the plan: any line that would fit another brief is a default. Rewrite it.
2. Tokens first. The first CSS block is :root with the palette, --t-display/--t-heading/--t-body/
   --t-meta, --r-1/2/3, --s-1/2/3, --shadow-rest/--shadow-lift. Every size references a token.
   The only literal outside :root is 0.
3. Hierarchy is contrast. The focal element is at least 3x its label. Four sizes per screen.
   One metric dominates; never six equal cells.
4. Banned: cream #F0EDE4-#FAF7F0 with terracotta #A84A14-#E08A5A; gradients; identical rounded
   cards; ALL-CAPS eyebrows; arrows on buttons; emoji as icons; entrance animation on every
   section; dark "because it is a dashboard". Pick the theme from the use scene and say why.
5. Economy: every element serves a decision or gets cut. Summaries over raw; one chart per screen;
   a region headline states meaning ("昨天有 3 处异常"), not a label. Name what you cut.
6. States: structural skeleton, not a spinner; empty = one sentence + one action; error = cause +
   next step, beside the failure. Every control changes the view or is deleted. Labels match data:
   14 days means 14 points. Deltas stay plausible; annotate spikes. Demo toggles live in their own
   labeled strip.
7. Tables: status column visible at 1440, no page-level horizontal scroll; rows 48-60px with
   secondary info inline; semantic color only on a dot, tag, or delta. Sticky = background + z-index.
8. Flows: one question per screen; a stepper shows progress and renders nothing; constraints as
   copy at the point of anxiety; primary action disabled until valid; one subtitle explains the
   process; a prefilled example in the input. Phone frame 375x812, taps really navigate.
9. Floor: real content; visible focus; button for actions, a for links; aria-label on icon
   buttons; 4.5:1 contrast; 16px body on mobile; 100dvh; tabular-nums; animate only transform
   and opacity, under 200ms, respect reduced-motion.
10. One self-check pass, fix once, ship. One index.html, inline CSS/JS, opens from file://.
    Hand over: the file, the direction and theme reason, what you cut, three things to verify
    with users.

## If you only have one minute

- Plan the user's one job, palette hexes and type ladder before CSS; put them in :root; no literal sizes outside it.
- Focal element 3x its label, four sizes per screen, one metric dominates.
- No cream + terracotta, no gradients, no card kit, no ALL-CAPS eyebrows, no arrows on buttons, no emoji icons.
- Skeleton, empty with one action, error with cause. Every control changes the view or is deleted.
- Every element serves a decision or gets cut. One self-check pass, then ship.
