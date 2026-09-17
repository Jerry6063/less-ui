# Run notes — less-ui v4 / brief 01 (ops dashboard)

## Files read
- `/Users/jerryhao/Dailywork/anker-ai-pilot-prep/skills-eval/.claude/skills/less-ui/SKILL.md` — ~11.5 KB
- `/Users/jerryhao/Dailywork/anker-ai-pilot-prep/skills-eval/briefs/01-ops-dashboard.md` — ~1.5 KB

Nothing else was opened. No reference files, no other skill dirs, no other runs.

Output: `index.html`, ~49 KB, single file, no CDN, opens from `file://` offline.

## Direction
Dark "instrument console" morning-check board (晨检作战台). Not a light SaaS card kit: one
48px revenue figure dominates, four supporting KPIs sit in a bordered strip (no six equal
cards), the alerts rail sits *beside* the table, and every KPI is derived from the row
dataset so filters recompute the headline honestly.

## `:root` token block (verbatim)

```css
:root{
  --surface:#10151A;
  --panel:#171E25;
  --panel-2:#1D262F;
  --ink:#E7EDF3;
  --muted:#93A2B2;
  --line:#28323C;
  --accent:#4C86E8;
  --ok:#4FA07A;
  --warn:#D9A23F;
  --alert:#DE6152;
  --t-display:48px;
  --t-heading:22px;
  --t-body:14px;
  --t-meta:12px;
  --r-1:3px;
  --r-2:8px;
  --r-3:14px;
  --s-1:8px;
  --s-2:16px;
  --s-3:32px;
  --s-half:4px;
  --shadow-rest:0 1px 0 rgba(0,0,0,.45);
  --shadow-lift:0 18px 48px rgba(0,0,0,.6);
  --font-ui:"IBM Plex Sans","PingFang SC","Hiragino Sans GB","Microsoft YaHei",sans-serif;
  --font-num:"IBM Plex Mono","SF Mono","PingFang SC",monospace;
  color-scheme:dark;
}
```

Tier math: display 48 = 4x meta 12 (>= 3x required); heading 22 >= 1.5x body 14 (21).
Mobile query at 760px redefines `--t-*` and `--s-3` only (the sanctioned literal exception).

## Build passes and self-check
- **Build passes: 1.** One `Write`, no rewrite.
- **Self-check: 1 pass, 1 fix.** Grepped the stylesheet for literal `font-size / border-radius /
  box-shadow / gap / padding / margin` outside `:root`: only two hits, both `0` (allowed). The one
  real fix was in the hand-drawn SVG charts — axis and annotation `<text>` elements carried
  `font-size="11"` as an SVG attribute; all 5 became `style="font-size:var(--t-meta)"`. No second
  review cycle was run.

## Controls wired to real data changes
Wired (each one moves the numbers on screen):
- **渠道 / 站点 selects** — filter the row set; the 48px revenue figure, all four KPIs, the
  weighted inventory-days-cover, the trend chart (scaled by revenue share) and the alerts rail
  all recompute.
- **对比口径 (环比上周 / 环比上月)** — every row carries separate WoW and MoM growth factors, so
  previous-period values, every delta chip, and the table's 环比 column all change; the sort key
  `delta` sorts on whichever period is active.
- **搜索框** — matches channel, market code, Chinese market name, SKU code and SKU name; filters
  table + alerts + KPIs; zero results offers 清除全部筛选.
- **8 sortable columns** — toggle asc/desc, `aria-sort` set, caret direction flips.
- **趋势指标 (营收/订单/广告花费/ROAS)** — four distinct series; orders derive from AOV $50.6,
  ROAS derives from revenue/ad per day, so they stay internally consistent.
- **时间窗 7 天 / 14 天** — 14 authored daily points; the caption states the window, the date
  range and the point count, and the axis renders exactly that many points.
- **重新同步** — fires a real loading state, then restores and updates the timestamp.
- **Rows / alerts** — row click or Enter/Space opens the SKU drawer; alert click opens the alert
  drawer, whose 查看 SKU 下钻 button swaps to the SKU drawer.
- **Demo strip** (separate dashed strip, labeled 演示) — 正常 / 加载中 / 空数据 / 接口错误 drives
  skeletons, empty states and per-region error boxes for all three data regions.

Deleted rather than faked: no date-range picker (it would have needed a second month of data I
had no budget to author, and a picker that returns the same rows is the classic dead control);
no export/settings dialogs beyond a toast confirmation; the rail's secondary nav items are
labeled but do not pretend to be separate pages.

Numbers: headline deltas come out at +3.0% revenue, +2.2% orders, +13.7% ad spend, -9.4% ROAS
(the ROAS delta is arithmetically implied by the other two, not invented). The one large number,
Shopee PH ad spend +34.2%, is exactly the anomaly the third alert explains. The chart carries a
one-line annotation at 09-12 naming the 秒杀 campaign that caused both the revenue peak and the
ad-spend spike.

## What the skill cost in time
- Section 1's "write the plan, then attack it" plus section 2's palette-hex check took real
  thinking time up front — roughly a third of the run went to direction before any code, mostly
  to avoid the blocked cream/terracotta and to find an accent that does not collide with the
  ok/warn/alert semantic set.
- Section 5's "controls must be honest" forced the data model to be derived rather than authored
  per view: every row carries WoW and MoM growth factors and the aggregates are computed. That is
  slower to write than hardcoding a KPI strip, but it is why the filters are defensible.
- Section 2's ban on sparklines and the CDN-free requirement meant hand-rolling the SVG line
  chart (axis, gridlines, annotation, tooltips) instead of dropping in Chart.js — maybe 60 lines
  of extra JS, but it also guarantees the file works offline by double-click.

## Not finished / knowingly skipped
- **Extreme-data stress at 50 rows**: the dataset ships 9 channel-by-market rows (the real
  cardinality of 4 Amazon + 5 Shopee markets). The table region is scroll-capped and the name
  cell truncates, so 50 rows would hold, but it is not demonstrated.
- The **40-character product name** case is covered in the SKU drawer header (A1652's full name)
  and truncated inline in the table, but there is no 7-figure revenue row to prove the tabular
  number column never reflows.
- Review themes and warehouse inventory exist for 3 SKUs only; rows map onto those 3 rather than
  each having a unique SKU record.
