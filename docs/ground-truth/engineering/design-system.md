# E.C.H.O. — Design System

Status: team visual decisions recorded; accessibility palette adaptations authorized, implementation defaults pending PM approval and bootstrap validation.
Source: collective Design System survey, 2026-11-25 (one response, 39 questions).
Scope: web, Android and iOS. Read [Technology Stack](tech-stack.md), [Coding Conventions](coding-conventions.md) and relevant RAD/SDD artifacts. Agents must not modify this document or its brand assets. Visual choices do not override approved functionality, permissions or safety constraints.

## 1. Visual direction (team decisions)

- Material Design 3 as visual reference, not a mandated component library or unmodified Material theme. Use E.C.H.O.'s custom palette; light theme only. No automatic wallpaper-derived colors or dark theme.
- Welcoming, empathetic identity; existing logo unchanged and discreet on operational pages. Roboto, balanced typography and density, moderately rounded shapes, filled icons.
- Filled primary buttons, outlined secondary buttons; subtle card elevation; outlined input fields. Use shared components and consistent state treatments across targets.

### Brand assets

Canonical assets are in [assets/](assets/). Preserve their artwork, colors, proportions and transparency; do not redraw, recolor, stretch or crop the brand. Use the SVG originals when supported, or the supplied PNG equivalents. Copy or derive platform resources from these sources without modifying the canonical files.

| Asset | Use |
|---|---|
| `assets/logo_echo.svg`, `assets/logo_echo.png` | Standalone brand mark |
| `assets/full_logo.svg`, `assets/full_logo.png` | Full wordmark on a sufficiently dark background; use the standalone mark on light surfaces when needed |
| `assets/favicon.ico`, `assets/favicon-16x16.png`, `assets/favicon-32x32.png` | Browser favicon |
| `assets/apple-touch-icon.png` | Web home-screen icon for Apple devices |
| `assets/android-chrome-192x192.png`, `assets/android-chrome-512x512.png` | Web manifest icons, not final native launcher assets |
| `assets/site.webmanifest` | Web manifest reference; integrate with the actual deployment paths if applicable |

Existing brand gradients are exempt from the restriction on decorative UI gradients. Native launcher icons must be prepared from approved brand artwork at bootstrap (including appropriate 1024 × 1024 artwork and Android adaptive-icon layers); the supplied web icons do not establish native release readiness. Web manifest inclusion does not authorize offline caching or persistence of conversation content. Do not introduce PWA behavior solely because a manifest is available.

## 2. Color tokens (team palette with accessibility adaptations)

| Token | HEX | Role |
|---|---|---|
| `primary` | `#663399` | Brand, main action, active emphasis |
| `secondary` | `#7851A9` | Secondary emphasis |
| `accent` | `#702670` | Selected highlights |
| `background` | `#F6F4F8` | Page background |
| `surface` | `#FFFFFF` | Cards and containers |
| `text` | `#32174D` | Main text |
| `mutedText` | `#6D5B80` | Secondary text |
| `border` | `#D8BFD8` | Decorative borders and separators |
| `controlBorder` | `#9B7AA2` | Interactive control outline |
| `success` | `#147D58` | Positive outcome |
| `warning` | `#8A6100` | Warning |
| `danger` | `#D21F40` | Error and critical action emphasis |

Use semantic aliases rather than copying HEX values into screens. Error and danger share the adapted color but have distinct labels, icons and meanings. Accessibility adaptations supersede the survey values for success, warning and danger; all other survey colors are unchanged. `controlBorder` is an additional functional token.

### Accessible color pairings

Use the WCAG 2.2 AA contrast thresholds as an engineering target across platforms: at least 4.5:1 for normal text, 3:1 for large text and necessary non-text component/state indicators. Check actual adjacent colors, including state variants. This is not a claim of full WCAG conformance.

| Use | Foreground | Background / adjacent color |
|---|---|---|
| Body and muted copy | `text` or `mutedText` | `surface` or `background` |
| Filled brand action | `surface` | `primary` (or `secondary` / `accent` where appropriate) |
| Outlined secondary action | `primary` | `surface` or `background` |
| Filled semantic action or message | `surface` | `success`, `warning` or `danger` |
| Semantic text, icon or outline | `success`, `warning` or `danger` | `surface` or `background` |
| Input outline | `controlBorder`; `primary` when focused; `danger` on error | `surface` or `background` |

The adapted semantic tokens have contrast ratios of 5.12:1, 5.54:1 and 5.24:1 against `surface`, and 4.68:1, 5.07:1 and 4.79:1 against `background`, respectively. Use white (`surface`) text on their filled variants, not `text` (dark purple). The light `border` token is decorative only; use `controlBorder` for necessary control boundaries (3.69:1 against `surface`, 3.37:1 against `background`). Use a distinct visible focus indicator with sufficient contrast against adjacent colors. Never rely on color alone. Do not invent substitute palette colors in individual features. Check actual rendered states, including opacity and overlays.

## 3. Foundation defaults (proposed; not survey values)

Use logical units (dp on native, CSS px on web at the default scale); text must scale with user settings. Values below refine the qualitative team choices. Centralize them in a shared typed theme at bootstrap; do not duplicate literal values across screens.

| Token group | Values / usage |
|---|---|
| Spacing | 4, 8, 12, 16, 24, 32; default card padding 16, screen padding 16 compact / 24 wider |
| Shape | Small 8 (inputs), medium 12 (buttons/cards), large 16 (larger surfaces) |
| Typography | Roboto; caption 12/16, label 14/20, body 16/24, section title 20/28, screen title 24/32 (size/line height); weights 400/500/600 |
| Interactive area | At least 48 x 48 logical units; expand when text wraps |
| Elevation | One shared subtle card shadow (platform equivalent); no heavy shadows or decorative gradients |
| Adaptive layout | Compact <600; medium 600–839; expanded >=840 logical units; reflow without horizontal scrolling |
| Motion | Short, nonessential transitions, default 150–200 ms; suppress nonessential motion when reduced motion is requested |

Use a single column for compact card grids and additional columns only when content and accessibility allow. Do not truncate required text or hide critical controls at larger font scales. The exact platform shadow mapping and font assets are shared bootstrap configuration, not feature-level choices.

## 4. Components and states

| Component | Rule |
|---|---|
| Button | Filled primary, outlined secondary. Critical actions use a distinct visible text label and filled icon; use `danger` with white text/icon for filled critical buttons, or an accessible outlined treatment in §2. |
| Card | Surface, moderate radius and subtle elevation; consistent spacing. |
| Input | Outlined, persistent label, accessible error text; placeholder is not a label. |
| Notification | Contextual banner for ongoing/relevant information; temporary toast only for noncritical outcomes. Critical notices remain perceivable until resolved/acknowledged as specified; fallback notices must not block communication. |
| Progress | Show stages only when actual stages are known; otherwise show an indeterminate indicator and truthful status. No fabricated percentage or wait estimate. |
| Icons | One filled icon family, accessible labels on icon-only controls; critical actions also have visible text. |

Use meaningful default, pressed, focused, disabled, loading, error and empty states where applicable; web also supports hover and keyboard focus. Disable only when behavior warrants it. Avoid hiding existing data or actions behind decorative loading. Use shared accessible primitives; do not create screen-specific versions of the same component.

## 5. Navigation and role layouts (team decisions)

- Helper and Supervisor desktop: labeled sidebar. Mobile: bottom navigation bar for authorized primary destinations; provide additional authorized destinations accessibly when needed. Caller: essential navigation always visible; mobile presentation follows bottom navigation where applicable.
- Caller, Helper and Supervisor dashboards: responsive card grid. Prioritize the role's core actions and current operational status; do not add dashboard metrics, permissions or features solely to fill a grid.
- Listening session: minimal, communication-centered layout; prioritize chat/audio and approved session controls. Respect safe areas, keyboard and font scaling. Keep applicable Safe Escalation control visible without scrolling on every session screen; navigation or overlays must not obscure it. Do not expose it to unauthorized actors.
- Safe Access Path: adapt the same visual system to the approved guest flow. Do not assume registered-user navigation or feedback obligations apply to guests.
- Routes, actions, visible information and workflow conditions derive from approved specifications; this document defines presentation, not additional routes or privileges. See [RAD use cases](../requirements/rad/use-cases/) and [navigation models](../requirements/rad/diagrams/navigation/).

## 6. Language and safety

- Caller copy: empathetic, informal, direct (e.g. “Ciao! Siamo qui per ascoltarti.”). Helper/Supervisor copy: professional and concise. Preserve approved Italian UI terminology; no unsupported promises of professional or emergency support.
- Use light illustrations only in welcome and empty states. Avoid decorative distractions in active listening or escalation. Respect reduced motion.
- Apply [RAD usability requirements](../requirements/rad/non-functional/requirements.md): `RNF_U_1` (GULPEASE >80), `RNF_U_2` (escalation control visible without scrolling), `RNF_U_3` (specified core actions within three interactions), `RNF_U_4` (responsive, required browsers, no horizontal scrolling).
- Apply `RNF_A_3`, `RNF_A_4`, `RNF_L_3`, `RNF_L_4` and `RF_SE_1`, `RF_SE_3`, `RF_SE_5`: preserve communication continuity, confidentiality, informed use and non-blocking fallback. Do not persist communication content or show unnecessary personal information in UI, notifications or test artifacts. Follow [known issues](../requirements/rad/known-issues.md); do not invent recovery or escalation semantics.
- Provide meaningful accessible names, roles and states, visible focus, logical keyboard order on web and screen-reader support on native. Do not communicate status by color, animation or sound alone.

## 7. Implementation and verification

- At bootstrap, select a compatible shared UI approach and icon family; load Roboto consistently on all targets. Use the canonical brand assets in §1; configure runtime asset locations at bootstrap. Do not introduce a competing UI library or change the brand independently. Theme code implements this document; configuration owns mechanical platform mapping.
- Planner includes relevant visual constraints and testable criteria in UI plans. Implementer reuses shared tokens/components. Independent Tester derives behavioral and accessibility checks from approved specifications, not rendered implementation. Reviewer checks conformance; use existing repair and audit paths without adding agent roles.
- Prefer deterministic checks: validate declared color pairings in unit tests; verify component labels/states and role-specific interactions using the existing test toolchain. Check responsive layout, critical control visibility and keyboard navigation in relevant web/native integration tests. Use synthetic data; do not capture real conversation content. Include affected shared consumers when a theme change is authorized.
- Automated accessibility checks can supplement the existing CI after bootstrap validation. No mandatory pixel-perfect snapshot comparison or separate design gate is introduced here. Visual review may use relevant screenshots as evidence, not as an independent source of requirements. Use existing CI commands and machine-readable reports; do not weaken tests to pass. Native/device behavior requires appropriate platform evidence.
- Pending: PM approval of §3 defaults; UI library/icon family and runtime asset integration (including native launcher assets); alignment with finalized SDD/DPD and TP/TCS; runtime checks across targets. Do not treat these pending details as confirmed survey decisions. Escalate only material uncertainty under the existing pipeline policy.

## References

- Team survey: E.C.H.O. — Design System | Decisioni del team, collective response dated 2026-11-25. Palette reference: https://coolors.co/663399-7851a9-702670-f6f4f8-ffffff-32174d-6d5b80-d8bfd8-2cc98f-fbbf24 (original team palette; survey semantic colors: success `#2CC98F`, warning `#FBBF24`, danger `#F32B4C`; superseded by the accessibility adaptations in §2).
- Project: RAD v1.0.0, [Technology Stack](tech-stack.md), [Coding Conventions](coding-conventions.md).
- [Material Design 3](https://m3.material.io/), [WCAG 2.2](https://www.w3.org/TR/WCAG22/), [React Native accessibility](https://reactnative.dev/docs/accessibility).
