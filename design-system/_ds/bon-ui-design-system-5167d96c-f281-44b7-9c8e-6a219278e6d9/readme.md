# BON UI Foundation Library — Design System

BON UI is the foundation design system for a **mobile-first Korean content platform** — a
news / entertainment / sports / shopping portal in the lineage of large Korean super-apps.
It is built around the **Pretendard** typeface, a signature **green (#03C75A)** brand color,
a blue secondary, and a deep semantic token system that spans **light + dark themes** and
**platform modes** (mobile / tablet / PC, iOS / Android, brand).

This project is the machine-readable design system: global CSS tokens, webfont declarations,
React component primitives, foundation specimen cards, and a full interactive UI kit. An
automated compiler bundles the components into a runtime library (`window.BONUIDesignSystem_5167d9`).

## Source

- **Figma:** “BON UI Foundation Library.fig” (attached, mounted read-only). Pages: Color,
  Typography, Shape, Layout-TBD (product screens), Design-Tokens, Version.
- Tokens, icons, and component specs were extracted directly from the Figma file
  (`fig_materialize`) — it is the source of truth, not any public brand spec.

---

## CONTENT FUNDAMENTALS — how copy is written

The product is **Korean-language, mobile, consumer-facing**. Copy is concise and scannable.

- **Language & voice.** Primary UI language is Korean. Labels are short noun phrases
  (`홈`, `뉴스`, `검색`, `구독`, `더보기`, `전체삭제`) rather than full sentences. Buttons use
  imperative/short forms (`담기`, `저장`, `+ 구독`).
- **Person.** Neutral/system voice — no first person. The user is rarely addressed directly;
  the UI states facts (`최근 검색`, `인기 검색어`, `관련 기사`).
- **Casing.** Korean has no case. Latin/acronym labels are uppercase when they are brand or
  tags (`BON`, `LIVE`, `NEW`, `MY`). English running text is sentence case.
- **Numbers & metadata.** Heavy use of compact metadata: relative time (`2시간 전`, `32분 전`,
  `어제`), counts (`조회 12만`, `댓글 64`), ranks (`1위`). Counts abbreviate with 만/억.
- **Tone.** Informative, trustworthy, lightly energetic on entertainment/shopping surfaces
  (badges like `LIVE`, `42%`), calm and factual on news.
- **Emoji.** Not used in product chrome. Status is conveyed with badges, icons, and color —
  never emoji.
- **Punctuation.** Middot `·` separates metadata. Hash `#` prefixes keyword tags (`#맛집`).

---

## VISUAL FOUNDATIONS

- **Color.** Neutral-dominant canvas (white surfaces on a light-gray `#F0F0F0` app background)
  with the green brand color reserved for primary actions, selected states, and brand moments.
  Blue is secondary/links. Status palette: green=success, blue=info, orange=warning, red=danger.
  Every color is a semantic token (`--neutral-foreground-default`, `--primary-background-default`,
  `--secondary-foreground-default`, …) backed by a 0–1600 / 100–1200 numeric ramp.
- **Type.** Pretendard across the board, tracking tuned to **-0.3px** for Korean. Five roles:
  Display (hero) → Heading (titles) → Label (controls) → Paragraph (body) → Detail (caption).
  Weights 400/500/600/700/800. Minimum UI text ~11px (detail), body 15–16px.
- **Spacing.** 4-based scale exposed as `--spacing-2xs(6) … 3xl(28)` plus layout spacing.
  Modules use 20px vertical / 16px horizontal padding; card grids gap 8–12px.
- **Radius.** Soft, friendly corners: `2xs 4 · xs 6 · s 8 · m 12 · l 16 · xl 20 · full 999`.
  Controls 8, cards/thumbnails 12–16, chips/avatars/badges full.
- **Backgrounds.** Flat color fills — **no decorative gradients**. Imagery is the visual
  energy: full-bleed thumbnails with rounded corners, often in 1:1 / 3:4 / 16:9 ratios.
  Section modules sit on white cards separated by thin gray gaps / `thick` dividers.
- **Elevation.** Mostly flat. Cards lift with a soft two-layer shadow
  (`0 1px 2px rgba(0,0,0,.04), 0 4px 16px rgba(0,0,0,.06)`); toasts/sheets go deeper.
  Borders are hairline alpha-black (`--neutral-stroke-subtle-1/divider`).
- **Animation.** Quick and restrained — 120ms color/opacity transitions, 180ms switch thumb
  with a gentle cubic-bezier. No bounces or infinite loops.
- **Hover / press.** Hover = subtle dimmed-ghost layer (`rgba(0,0,0,.03)`) or a darker tone
  step on filled buttons. Press = `scale(.98)` on buttons, `scale(.94)` on icon buttons.
- **Transparency & blur.** Alpha-black/white scales power overlays, scrims (backdrop 40–50%),
  and dimmed state layers. Blur is reserved for sheet/scrim backdrops.
- **Cards.** White surface, radius 16, hairline border *or* soft shadow (not both), optional
  16px padding. Thumbnails clipped to radius 12.

---

## ICONOGRAPHY

- **System.** A custom in-house line/fill icon set (extracted from Figma as
  `assets/icons/icon-data.js`, 149 glyphs on a 24×24 grid). Each concept ships in two
  **types** — `outlined` and `filled` — and outlined has three weights (`light`/`medium`/`bold`).
- **Usage.** Outlined-medium is the default; `filled` marks active/selected states
  (e.g. the active bottom-nav tab, liked/saved reactions). Render via the `Icon` component:
  `<Icon name="search" />`, `<Icon name="home" type="filled" />`.
- **Color.** Single-color, painted with `currentColor` — recolor by setting `color`.
- **Coverage.** Navigation (home, search, back, forward, menu, more), content (news, chatting,
  play, keep, like, calendar, booking, location, shoppingBag, placeBookmark), status (alert,
  exclamationMark, checked, done, close, cancel), and the **N brand logo** (`nLogo`).
- **Emoji / unicode.** Not used as iconography anywhere.
- Need an icon that isn’t present? Re-materialize from the Figma file (don’t hand-draw SVGs).

---

## INDEX — what’s in this system

**Global CSS** — link `styles.css` (it `@import`s everything below):
- `tokens/fig-tokens.css` — 3,619 Figma Variables (light `:root` + dark + 14 platform/theme scopes)
- `tokens/fig-typography.css` — generated text/effect styles
- `tokens/fonts.css` — `@font-face` (Pretendard, NanumSquare Neo) + family aliases
- `tokens/base.css` — reset + document defaults
- `tokens/typography.css` — `.bon-{display|heading|label|paragraph|detail}-{size}` classes
- `components/bon-components.css`, `components/bon-components-2.css` — component styles

**Components** (`window.BONUIDesignSystem_5167d9`):
- Core — `Button`, `IconButton`, `ButtonGroup`, `Badge`, `Bubble`, `Tag`/`TagGroup`,
  `Chip`/`ChipGroup`, `Avatar`, `Dot`, `Divider`, `Card`, `Icon`
- Forms — `TextField`, `Checkbox`/`CheckboxGroup`, `Radio`, `Switch`, `Slider`
- Feedback — `AlertBanner`, `Toast`, `Clue`, `Tooltip`
- Navigation — `Tabs`, `NavigationBar`, `BottomNav`

**Foundation cards** — `guidelines/*.card.html` (Colors, Type, Spacing, Brand groups).

**Icons** — `assets/icons/icon-data.js` + `components/core/Icon.jsx`.

**UI kit** — `ui_kits/content-app/` — interactive mobile content app (home feed, search,
article) composing the primitives. Entry: `ui_kits/content-app/index.html`.

**Skill** — `SKILL.md` (Agent-Skills compatible).

---

## CAVEATS / SUBSTITUTIONS

- **Fonts:** Pretendard & NanumSquare Neo load from public CDNs (OFL). **SF Mono** (Apple,
  proprietary) is substituted with a system-mono + JetBrains Mono stack for spec specimens.
  Some Figma platform tokens reference iOS/Android system fonts (`Apple SD Gothic Neo`,
  `Roboto`) that fall back to the system stack until those binaries are supplied.
- **Imagery:** the UI kit uses tinted placeholder blocks (no real/copyrighted media).
