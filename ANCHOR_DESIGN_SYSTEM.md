# Anchor Design System — v2.0 (WCAG 2.2 AA)

> **Source of truth:** `design-system.html` in this repo (navigable shell); this file is the printable spec.
> Three static files, no build step. Shared `:root` tokens, DM Sans / DM Mono type, and one persistent theme (`anchor-theme`, OS default) across landing, docs, and design system.
> Owner: Fortunesoft IT Innovations — Internal Identity Platform.

## 1. Principles

1. **Centralized, not rebuilt:** Anchor owns *who a user is and when they may act*. Apps own *what a user can do*.
2. **Production-safe defaults:** Defaults work in sandbox; overrides are per-org and audit-logged.
3. **Stability signals everywhere:** Every page exposes area / stability / date. Beta and Deprecated are never silent.
4. **Compact developer density:** 13px body, 40px topbar, minimal chrome. Content first, decoration last.
5. **Same tokens everywhere:** Landing, docs, and design system reuse identical color, type, line, and radius tokens.
6. **Tokens over values:** no component references a raw hex. Brand (`--brand`) is immutable; functional (`--accent`) adapts per theme.
7. **AA conformance is built in:** every text/UI pair below is measured against WCAG 2.2 (4.5:1 text, 3:1 large text and non-text). Thinnest passing pair is 4.69:1.

## 2. Design Tokens

### 2.1 Color — light (default)

| Token | Value | Usage | Pair check |
|---|---|---|---|
| `--bg` | `#FFFFFF` | Page background | — |
| `--ink` | `#1B1F27` | Primary text, headings, code | 16.51:1 on bg ✅ |
| `--dim` | `#434C59` | Secondary text, descriptions | 8.69:1 ✅ |
| `--faint` | `#646D7A` | Tertiary text, labels, timestamps, kbd | 5.24:1 bg / 4.93 surface ✅ |
| `--surface` | `#F7F8FA` | Sidebar, panels, search, menus | — |
| `--raised` | `#F0F2F5` | Hover wash | — |
| `--line` | `#E3E6EB` | Decorative borders (cards, chrome) | exempt (never a sole boundary) |
| `--line-soft` | `#EDEFF2` | Decorative-only dividers | exempt (never a sole boundary) |
| `--line-strong` | `#767E8C` | Hover-intensified borders | 4.09:1 ✅ |
| `--input-border` | `#767E8C` | Form-control boundaries | 4.09:1 ✅ (1.4.11) |
| `--scroll-thumb` | `#878F9E` | 4px scrollbar thumb | 3.25:1 bg / 3.06 surface ✅ |
| `--accent` | `#045E96` | Links, active states, icons, focus | 6.89:1 ✅ |
| `--accent-soft` | `#E6F1F7` | Active pill/tab bg, selected rows | 8.11:1 w/ `--accent-ink` ✅ |
| `--accent-ink` | `#034A78` | Text on soft, link hover | 9.31:1 ✅ |
| `--brand` | `#045E96` | Button fill + shield logo, immutable | 6.89:1 w/ white ✅ |
| `--brand-ink` | `#034A78` | Primary-button hover | ✅ |
| `--ok` | `#1C7A52` | Success text, ticks, confirmations | 5.31:1 / 4.69 on fill ✅ |
| `--ok-bg` | `#E7F4ED` | Success fill | — |
| `--beta-ink/bg/line` | `#93610C / #FFF4E3 / #F2DDAF` | Warning | 5.31 / 4.88 ✅ |
| `--dep-ink/bg/line` | `#912018 / #FEF3F2 / #FECDCA` | Danger | 8.66 / 7.97 ✅ |
| `--error` | `#B42318` | Form validation | 6.57:1 ✅ |

### 2.2 Color — dark (`[data-theme="dark"]`)

Same names. `--accent` lightens to **`#258AC6`** (4.73:1, closest passing cerulean with margin — `#2286C2` at exactly 4.50 was rejected as borderline). `--brand`/`--brand-ink` stay `#045E96`/`#034A78`, so buttons and the shield show the true brand in dark mode. `--line` reverts to hairline `#2C323D` (decorative); form controls use `--input-border #6B7585` (3.86:1); `--line-strong` → `#6B7585`; `--scroll-thumb` → `#6E7889` (4.03/3.70). Status inks (`#3FBE85`, `#E0A63D`, `#F0776A`) all verify 6.0–8.8:1. Dark chart series: s1 `#258AC6`, s3 `#8B7CC2`, s6 `#C25375`, s7 `#8A95A5` (≥3:1); s2/s4/s5/s8 unchanged.

Copy-paste:

```css
:root{
  --bg:#FFFFFF;
  --ink:#1B1F27; --dim:#434C59; --faint:#646D7A;
  --surface:#F7F8FA; --raised:#F0F2F5;
  --line:#E3E6EB; --line-soft:#EDEFF2; --line-strong:#767E8C;
  --input-border:#767E8C; --scroll-thumb:#878F9E;
  --accent:#045E96; --accent-soft:#E6F1F7; --accent-ink:#034A78;
  --brand:#045E96; --brand-ink:#034A78;
  --beta-ink:#93610C; --beta-bg:#FFF4E3; --beta-line:#F2DDAF;
  --dep-ink:#912018; --dep-bg:#FEF3F2; --dep-line:#FECDCA;
  --ok:#1C7A52; --ok-bg:#E7F4ED; --error:#B42318;
}
[data-theme="dark"]{
  --bg:#14171C;
  --ink:#F3F5F7; --dim:#AEB6C2; --faint:#7A8494;
  --surface:#1B1F27; --raised:#232833;
  --line:#2C323D; --line-soft:#262B35; --line-strong:#6B7585;
  --input-border:#6B7585; --scroll-thumb:#6E7889;
  --accent:#258AC6; --accent-soft:#0F2E42; --accent-ink:#8AC7EE;
  --brand:#045E96; --brand-ink:#034A78;
  --beta-ink:#E0A63D; --beta-bg:#2E2410; --beta-line:#4A3A18;
  --dep-ink:#F0776A; --dep-bg:#331512; --dep-line:#4F1F1B;
  --ok:#3FBE85; --ok-bg:#0F2A1E; --error:#F0776A;
}
```

### 2.3 Typography

| Token | Value |
|---|---|
| `--sans` | `'DM Sans', ui-sans-serif, system-ui, sans-serif` |
| `--mono` | `'DM Mono', ui-monospace, SFMono-Regular, monospace` |

Body `13px/1.5`; hero `24px/600`; page title `20px/600`; section `13.5–14px/600`; mono labels `10–12px`. Sans for prose/UI, mono for code/versions/timestamps/kbd. Headings `600` only.

### 2.4 Spacing, radius, elevation, motion

- Base unit `4px`; container `1080px` landing / fluid article docs.
- Radius `4 → 6 → 8 → 10 → 12px` (pills → dialogs); `20px` rating pills; `999px` toggles/avatars.
- Shadows card/menu/overlay + `rgba(0,0,0,.35)` scrim (decorative).
- Motion `100/160/240ms`; honor `prefers-reduced-motion`.

### 2.5 Iconography

Lucide-style inline SVG, `stroke=currentColor`. Shield brand mark in `--brand` (logotype, contrast-exempt, identical both themes).

## 3. Layout shells

- **Landing:** `lp-top` 40px sticky (brand, Docs/Design System nav, theme toggle) + hero grid + footer grid.
- **Docs / Design System:** `196px sidebar | 1fr fluid article | 188px outline`, 40px topbar (brand, version, search, AI chat, tabs, theme toggle), in-column footer.
- Breakpoints `560/760/860/900/1080`; dialogs become bottom sheets <560px.

## 4. Components (selection)

- Buttons: `.btn` secondary, `.btn-primary` brand fill (white 6.89:1 both themes), `.btn-danger` error fill. No other button colors.
- Inputs `36px/44px mobile`, `1px --input-border` boundary (≥3:1 both themes), focus `accent` border + `accent-soft` ring; global `:focus-visible` = `2px --accent` outline.
- Nav leaves `12px`, active `accent-soft + accent-ink`; rows/cards/pager keyboard-operable (Enter/Space).
- Page tabs `Usage / Code / Style / Accessibility / Changelog` below the description (`36px`, `2px accent` underline on active, arrow-key nav, outline rebuilds per tab, Usage default).
- Status: stability chip beside the title; full area / stability / date strip lives in the `Changelog` tab.
- Overlays: modal 540–560px, confirm 420px, toast cap 3, CmdK max 40 rows, chat docked 340px.
- AI assistant: sparkle toggle → docked panel with 3 starter chips, cited mock answers (lightweight source chips via `selectPage`), 2 follow-ups per answer, thumbs + copy + timestamp row below each message (revealed on hover/focus), send icon-button disabled until typing, fallibility footnote below input; `Enter` sends, `Esc` closes, list is `aria-live polite`.
- Notifications & status — four statuses, one language (icons: Anchor stroke, never color alone):

  | Status | Usage | Anchor color | Icon |
  |---|---|---|---|
  | Informational | Extra info, not tied to the action | `--accent` | circle + i |
  | Success | Task completed as expected | `--ok` | circle + check |
  | Warning | Undesirable action / surprising result | `--beta-ink` | triangle + ! |
  | Error | Failure, may block until resolved | `--dep-ink` (never form-only `--error`) | circle + × |

  Variants: Toast (**built** — white, `2px` status border, 5s uniform dismiss, cap 3, `showToast(msg, status)` defaulting to `success`), Inline / Actionable / Callout (**spec only**).

## 5. Patterns

Sticky brand+nav+entry header; blur validation with `(required)` labels; filter pills; CmdK global search; hosted-login-only auth; skeleton/article loads; toast/banner/inline notification split; confirm every destructive action; truncate + tooltip overflow; PII masked with explicit reveal.

## 6. Data visualization

Bar/line default; 8-series categorical set (light values double as the documented ramp; dark overrides s1/s3/s6/s7 per §2.2). Axes `11px mono faint`, values on hover, never color alone (legend + labels always).

## 7. Content & voice

Direct, calm, specific; verbs on buttons; cause + next step on errors; absolute mono timestamps first; comparable numbers in mono.

## 8. Accessibility & compliance (WCAG 2.2 AA)

1. Contrast: text ≥4.5:1, large/UI ≥3:1 — full pair table in §2.1/2.2, thinnest 4.69:1.
2. Focus: visible `:focus-visible` ring on everything; skip link first in tab order; 56px scroll margin so sticky chrome never obscures focus (2.4.11).
3. Keyboard: tab order = visual order; all rows/cards operable; `Ctrl/⌘+K`, arrows, Enter, Esc ladder (feedback > chat > search).
4. Targets ≥24px (2.5.8); nav rows padded to 26px.
5. Never color alone; labels always visible; errors `role=alert`, confirmations `role=status`.
6. Destructive/permission actions always confirm. Target: WCAG 2.2 AA on all surfaces.

## 9. Theming

`[data-theme]` on `<html>`, key `anchor-theme`, OS default, blocking head script (no flash), sun/moon toggle in all three topbars. `--brand` is the only theme-invariant hue. White-labeling forks at Tier-1→Tier-2.

## 10. Do's and Don'ts

Do reuse tokens verbatim; DM Sans UI + DM Mono code; shield in `--brand` only; Beta/Deprecated in three places; skeletons for loads; 44px touch targets; confirm destructive actions; verify both themes; keep skip link + focus ring + keyboard rows.
Don't add accents or button styles; no 700 headings/gradients; no hidden version/stability; no SMS for new flows; no custom auth UI; no polling where webhooks exist; no color-alone meaning; no placeholder-as-label; no silent bulk actions; max 3 toasts; no hardcoded hex where a token exists.
