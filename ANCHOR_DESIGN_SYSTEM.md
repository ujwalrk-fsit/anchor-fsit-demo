# Anchor Design System

> **Source of truth:** `index.html` + `docs.html` in this repo.
> Two static files, no build step. Shared `:root` tokens and DM Sans / DM Mono type ensure landing and docs scale together.
> Owner: Fortunesoft IT Innovations — Internal Identity Platform.

## 1. Principles

1. **Centralized, not rebuilt:** Anchor owns *who a user is and when they may act*. Apps own *what a user can do*.
2. **Production-safe defaults:** Defaults work in sandbox; overrides are per-org and audit-logged.
3. **Stability signals everywhere:** Every page exposes area / stability / date. Beta and Deprecated are never silent.
4. **Compact developer density:** 13px body, 40px topbar, minimal chrome. Content first, decoration last.
5. **Same tokens everywhere:** Landing (`lp-*`) and docs reuse identical color, type, line, and radius tokens.

## 2. Design Tokens

### 2.1 Color

| Token | Value | Usage |
|---|---|---|
| `--ink` | `#1B1F27` | Primary text, headings, code text |
| `--dim` | `#5B6472` | Secondary text, descriptions, list rows |
| `--faint` | `#8B93A3` | Tertiary / placeholder, mono labels, timestamps, icons at rest |
| `--surface` | `#F7F8FA` | Sidebar bg, win-bar / dash-bar, search-big, cmdk-foot, panel |
| `--raised` | `#F0F2F5` | Hover wash for nav, tabs |
| `--line` | `#E3E6EB` | Borders: cards, inputs, topbar, sidebar |
| `--line-soft` | `#EDEFF2` | Subtle dividers inside lists, sections |
| `--accent` | `#045E96` | Primary action, links, active states, icon color |
| `--accent-soft` | `#E6F1F7` | Active pill / tab bg, selected cmdk row |
| `--accent-ink` | `#034A78` | Text on `accent-soft`, primary hover (`btn-primary:hover`) |
| `--ok` | `#1F8A5B` | Success, operational pill, helpful confirmation |
| `--beta-ink` | `#93610C` | Beta text |
| `--beta-bg` | `#FFF4E3` | Beta background |
| `--beta-line` | `#F2DDAF` | Beta border |
| `--dep-ink` | `#912018` | Deprecated text |
| `--dep-bg` | `#FEF3F2` | Deprecated background |
| `--dep-line` | `#FECDCA` | Deprecated border |

Copy-paste:

```css
:root{
  --ink:#1B1F27; --dim:#5B6472; --faint:#8B93A3;
  --surface:#F7F8FA; --raised:#F0F2F5;
  --line:#E3E6EB; --line-soft:#EDEFF2;
  --accent:#045E96; --accent-soft:#E6F1F7; --accent-ink:#034A78;
  --beta-ink:#93610C; --beta-bg:#FFF4E3; --beta-line:#F2DDAF;
  --dep-ink:#912018; --dep-bg:#FEF3F2; --dep-line:#FECDCA;
  --ok:#1F8A5B;
}
```

### 2.2 Typography

| Token | Value |
|---|---|
| `--sans` | `'DM Sans', ui-sans-serif, system-ui, sans-serif` |
| `--mono` | `'DM Mono', ui-monospace, SFMono-Regular, monospace` |

Load: `DM Sans 400/500/600/700` + `DM Mono 400/500` via Google Fonts with preconnect.

| Element | Spec | Usage |
|---|---|---|
| Body | `13px / 1.5, sans, ink on #fff, antialiased` | Global default |
| Hero `h1` | `24px / 600 / -0.01em / 1.25` | Landing hero, docs home hero |
| Page title | `20px / 600 / -0.01em / 1.25` | Article title |
| Section `h2` | `14px / 600` home, `13.5px / 600` article | `sec-title`, `lp-sec h2` |
| Description | `13px–13.5px, dim` | `page-desc`, `lp-sec .sub`, `feat-desc` |
| Mono label | `10–12px mono, faint` | `brand-sub`, `kicker`, `crumb`, `stat .l`, `act-row time`, `kbd` |
| Footer / meta | `11.5–12px, dim/faint` | `meta-min .mi`, `f-link`, `footer` |

**Rules:**
- Sans for prose and UI. Mono only for labels, versions, code, timestamps, status pills, kbd.
- Headings use `600` only. No `700` in UI except tick marks.
- Links: `accent`, underline on hover only.

### 2.3 Spacing, Radius, Border, Shadow

- **Page container:** `lp-wrap max-width 1080px, padding 0 20px, centered`.
- **Article container:** `content padding 16px 20px 28px, fluid width, max-width none`.
- **Topbar:** `height 40px, padding 0 10-12px, gap 8px, sticky top 0, z 30, 1px bottom border`.
- **Sections:** `lp-sec padding 28px 0, border-top line-soft`. Article `.sec margin 14px 0`.
- **Radius:** `4px` pills/kbd/tags → `6px` buttons/inputs → `8px` cards/lists/panels → `10px` windows/dash → `12px` dialogs/cmdk. `20px` for rating pills only.
- **Borders:** `1px solid line` for cards/inputs. `1px line-soft` for inner dividers. Callout: `1px line + 2px left accent` (deprecated variant: left `dep-ink`).
- **Shadows:** Cards `0 12px 32px rgba(16,24,40,.08)`, dash `0 16px 40px rgba(16,24,40,.10)`, menus/dialogs `0 8px 24px rgba(16,24,40,.12)`, overlays `0 24px 64px rgba(0,0,0,.25)`. Overlay scrim `rgba(0,0,0,.35)`.
- **Scrollbar:** `thin-scroll 7px, thumb line, radius 4px, transparent track`.

### 2.4 Breakpoints

| Width | Behavior |
|---|---|
| `1080px` | Docs `layout` drops right outline. `chat-open` collapses to `196px 1fr 320px`. |
| `900px` | `home-grid` 3→2 cols. `footer-grid` 5→2 cols. |
| `860px` | `lp-hero-grid`, `lp-two` 2→1 col. |
| `760px` | Hide `brand-sub`. |
| `560px` | `home-grid`, `footer-grid` →1 col. |

## 3. Layout Specs

### 3.1 Landing Shell

- `lp-top` 40px sticky bar: brand (17px shield + `Anchor` 13px/600 + mono sub) left, spacer, CTAs.
- `lp-hero-grid`: `1fr 1.05fr, gap 28px, padding 40px 0 28px`. Left copy + `cta-row gap 8px`. Right `dash` mock.
- `lp-two`: `1fr 1fr, gap 24px` — checklist left, `code-panel` right.
- Footer: `footer-grid 1.5fr 1fr 1fr 1fr 1fr, gap 24px 32px`, then `f-bottom` legal strip with `sep` dividers.

### 3.2 Docs Shell

- Grid: `196px minmax(0,1fr) 188px, height calc(100vh - 40px)`. Chat open: `196px minmax(0,1fr) 188px 340px`.
- Columns: `sidebar` (surface, right border, `8px 6px` padding) | `main-scroll` (flex column, footer sticks to bottom via `margin-top:auto`) | `outline` (left border, `14px 10px 20px 12px`).
- Topbar order: brand → version pill → spacer → search pill → AI button → topnav (`API Reference, SDKs, Roadmap, Release Notes, Status`).
- Article order: crumb → title-row → page-desc → meta strip → body sections → divider → helpful → pager → in-column footer.

## 4. Component Usage Specs

### 4.1 Buttons

| Variant | Spec | Use for |
|---|---|---|
| `.btn` | `12.5px sans, white bg, line border, 6px radius, 5px 13px padding, dim text` | Secondary CTAs, helpful Yes/No, dialog Close |
| `.btn-primary` | Same + `accent bg/border, white text` → hover `accent-ink` | Primary CTA, Send, Submit |
| `.icon-btn` | `12px, 4px 9px, line border` + 9px icon | Feedback dropdown, AI sparkle button (28×28) |
| `.rate-pill` | `20px radius, 3px 10px` → `.sel` gets `accent-soft bg + accent border` | Issue rating: none / not useful / needs work / good / great / awesome |

Do not invent new button colors. Primary is always accent. No ghost buttons except `fb-linkbtn` for Preview toggle.

### 4.2 Navigation

- **Version pill:** mono 11px, `28px` height, `6px` radius, chevron rotates on open. Menu `168px min-width, 8px radius`. Items show `ver-tag` for Current / v1 GA.
- **Search pill:** `28px` height, faint text + 13px icon + `kbd Ctrl+K`. Opens cmdk.
- **Topnav:** text buttons `12px dim`, `4px 8px`, `6px radius`. `.active` = `accent-soft bg + accent-ink text`.
- **Sidebar:** `details.nav-group` top-level open by default. `nav-sum.top 11.5px/600`, `nav-sum.sub 12px/500`, caret 8px rotates 90° on open. Children indented `margin 1px 0 3px 7px + padding-left 5px + left line border`. Leaf `12px dim, 3px 6px, 5px radius`. `.active` = `accent-soft + accent-ink + 500`.
- **Outline:** `10.5px uppercase faint h4`. Links `12px dim, 2px left transparent border`. `.active` = `accent-ink + accent left border + 500`. Hidden under 1080px or when empty.
- **Breadcrumbs:** mono 11px faint, `/` separators with 6px margins. Home is accent link.

### 4.3 Content Blocks

- **Kicker:** mono 10px `accent-ink on accent-soft, 4px radius, 1px 6px` — e.g. `v2026.09 — now live`.
- **Meta strip (`meta-min`):** top+bottom `line-soft` borders, `6px 0` padding, `4px 12px` gaps. Three items: area (doc icon) / stability (clock icon, colored text) / date `2026-08-14` in mono code. Stability text: `ok-t ok-green` Stable, `beta-t` Beta, `dep-t` Deprecated.
- **Status chips:** Title row `beta/dep 10px/600 mono`. Nav inline `beta-sm/dep-sm 9px`. List suffix `beta-inline/dep-inline 11px faint (Beta)/(Deprecated)`. Always pair chip + suffix + meta strip — never chip alone.
- **Callout:** `surface bg, 8px radius, 9px 12px, 13px dim`. Default left `accent`. Deprecated variant left `dep-ink` with bold `Deprecated.` lead.
- **In-list:** `8px radius, line border`. Row `6px 10px, 13px dim, top line-soft divider (first none)`. Hover `surface bg + ink text`. Right 12px chevron faint→dim.
- **Home/pillar card:** `8px radius, 10px padding, white bg`. 18px accent stroke icon, `13px/600 title`, `11.5px/1.45 dim desc`. Hover `accent border` only. Click goes to docs.
- **Bullets:** `ul.bul 18px left padding, dim 13px, 3px row gap`. Bold inline = ink.
- **Divider:** `1px line, 14px vertical margin`.

### 4.4 Code & Windows

- **Code panel:** `line border, 8px radius, white bg`. Tabs bar `surface bg, bottom line border, 5px 6px padding`. Tab `12px dim, 4px 10px, 6px radius`. `.active` = `accent-soft + accent-ink`. `pre 14px padding, 12px mono, 1.6 line-height, min-height 180px (150px inside win)`.
- **Capability window (`win`) / dashboard (`dash`):** `10px radius, white bg, line border`. Bar `surface bg, 8px 12px, 9px dots + 11px mono title`. Dashboard adds `dash-pill 10px mono ok-green on #E7F4ED` + `stat-grid 3 cols, 8px gap` (`stat 8px radius, 8px 10px, 15px/600 number + 10px mono faint label`) + `act feed` (`7px dot ok/amber, 11px mono code, 10.5px mono faint time`).

### 4.5 Overlays

- **CmdK:** overlay fixed, `10vh` top padding. Dialog `540px, 12px radius`. Head `10px 12px` with 15px icon + borderless 14px input + Esc kbd. Results `340px max-height, 5px padding`. Row `6px 9px, 6px radius`; `.sel` = `accent-soft`. Right `parents 11px mono faint, 170px max`. Footer `surface, 11px faint` with kbd hints. Behavior: `Ctrl/⌘+K` toggle, `↑↓` navigate, `Enter` select, `Esc` close, filter by title + parents, max 40 rows.
- **Feedback dialog:** overlay `6vh` top padding. Dialog `560px, 12px radius`. Head `12px 14px` with title 14px/600 + sub 12px dim. Body `12px 14px, 62vh max-height, scroll`. Fields: Summary required text, Description textarea `58px min-height` + Preview toggle + file attach + sensitive Yes/No required + Name/Email. Errors `12px #B42318`. Actions right-aligned on surface bar. Success replaces body with `✓ Thanks — logged...` tagged to page.
- **Helpful widget:** inline `Was this page helpful? Yes/No`. Yes → `✓ Thanks`. No → panel with textarea + Submit → `✓ logged`.
- **AI chat:** docked 4th grid column, `340px (320px <1080px)`, left border. Head with sparkle icon + title/sub + X. Messages on surface bg, bubbles `8px radius, white, 85% max-width`; `.me` right-aligned with accent border + ink text. Input bar top-bordered with Send. Toggle via topbar, close via X or Esc. Esc priority: feedback > chat > cmdk.
- **Pager:** flex space-between. Link with 12px chevron + `pager-k 10.5px faint (Previous/Next)` + `pager-t 12.5px/500 dim → accent-ink on hover`.

### 4.6 Roadmap & Releases

- **Phase card:** `8px radius, 10px 12px, 8px bottom margin`. Head baseline split: `13.5px/600 title` + `11px mono faint date`. List rows with `pill 10.5px mono accent-ink/accent-soft` (`.gray dim/raised`, `.amber beta` for In progress).
- **Release:** `2px left line border, 14px left padding, 16px bottom margin`. Dot `8px accent at -5px/5px`. `ver 13px mono/600 + date 11.5px faint`. Items with `tag 10px mono faint bordered` (New / Improved / Fixed / Security).

### 4.7 Footer

Docs in-column footer: `12px dim, 12px 20px padding, top line border, surface? white bg`. Links dim → `accent-ink underline` on hover, `|` separators in line color, copy `faint, margin-left auto`.
Landing footer: same + 5-col grid above with `f-brand 13px/600`, `f-tag 12px dim 260px max`, `f-head 12px/600 ink`, `f-link 12px dim`.

## 5. Iconography

- Inline SVG only, `display:block`, `stroke=currentColor`, `fill=none`, round caps/joins.
- Sizes: nav caret 8px, pager/icon-btn 9-12px, sidebar home 13px, search/chat 13px, outline meta 12px, brand 17px, pillar 18px.
- Stroke: `1.6px` cards/brand, `1.8px` meta/chat, `2–2.4px` carets/chevrons/search.
- Brand mark: shield `M12 2L4 6V12C4 17 7.5 21 12 22C16.5 21 20 17 20 12V6L12 2Z` + circle + stem, always `#045E96`.

## 6. Do's and Don'ts

### Do

- Do reuse `:root` tokens verbatim. No hex outside tokens except overlay scrim and `#B42318` for form errors.
- Do keep topbar at 40px and sticky. Keep sidebar at 196px and outline at 188px.
- Do use DM Sans for UI/prose, DM Mono for code/versions/timestamps/kbd/pills.
- Do show Beta/Deprecated in three places: chip in title, suffix in nav/lists, colored label in meta strip.
- Do use `in-list` rows for In this section / Related / Popular guides. Keep row pattern: label left, chevron right.
- Do use callouts for deprecations and reprioritization requests with link to migration/deprecation policy.
- Do keep dialogs at 540–560px, 12px radius, surface action bar, Esc to close.
- Do keep `thin-scroll`, scroll-spy, and `Ctrl+K` behavior consistent.
- Do hover with `border-color: accent` + text `accent-ink` for cards/links/buttons. Use `surface` wash for nav rows.

### Don't

- Don't introduce new accent colors, new button styles, or filled dark code blocks — code stays white bg with mono ink.
- Don't use `700` headings, drop shadows on text, or gradients.
- Don't hide version (`v2026.09` current), date (`2026-08-14` pattern), or stability — every article needs the meta strip.
- Don't use SMS fallback for new flows — it is Deprecated. Point to WebAuthn/passkeys.
- Don't build custom auth UI when hosted login + SDK covers it. Don't poll when webhooks cover lifecycle events (create/disable/role change).
- Don't add outline entries that don't map to `section[id]`. Don't leave empty outline visible — hide it.
- Don't break keyboard order: feedback overlay Esc first, then chat Esc, then cmdk Esc. Don't trap focus without Esc.
- Don't exceed `1080px` content width on landing. Don't let article content set `max-width` — it is fluid by design.
- Don't use emoji in UI. Status is conveyed by color + mono label, not icons alone.
