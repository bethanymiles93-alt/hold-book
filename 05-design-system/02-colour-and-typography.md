# Colour and typography

## Colour principle

Colour psychology is often oversimplified and culturally dependent. Select colour through:

1. brand fit
2. accessibility
3. usability
4. user testing
5. emotional response

Do not choose a palette solely because “blue means trust” or “green means calm.”

## Proposed direction

- Warm off-white or cream background
- Deep charcoal or dark blue-grey text
- Muted sage or blue-green secondary surfaces
- Restrained warm yellow for hope
- Clear accessible error colour
- Distinct focus and selected states

## Requirements

- Body text: at least 4.5:1
- Large text: at least 3:1
- Controls and meaningful graphics: at least 3:1
- Colour must not carry meaning alone
- Test dark mode separately

## State-based palette (Taking Time)

Carries the "settling inward / opening outward" motion metaphor (see `01-design-direction.md`) into colour:

- **Normal:** fresh off-white background, standard sage/green.
- **Taking Time:** subtly warmer, golden-hour-toned background and a slightly deeper, richer green — applied consistently across every screen shown during this state, not just the home circle. Never orange, sepia or an obvious filter effect; text must stay fully legible at all times.
- **Reconnect:** gradual return to the Normal palette as the circle expands — the visual equivalent of sunrise.

The change should read as environmental, not decorative — most users shouldn't consciously register it, only feel it.

## Selection-state colour semantics

Used on Circle-picker pills and equivalent selectable cards:

| Treatment | Meaning |
|---|---|
| Strong/primary green fill | Primary or most important item (e.g. Close Circle) |
| Soft sage fill | Standard selectable item |
| Dark green border | Selected (must not rely on fill/colour change alone — pair with a checkmark or equivalent) |
| White/outlined pill | Secondary navigation, add or manage action (e.g. "+ New Circle," "Manage your Circles") |

Keep the palette restrained — primary fill, soft fill, border, outline is enough vocabulary; adding more shades of green reduces clarity rather than adding it.

## Typography criteria

Choose a typeface that:

- remains clear at small sizes
- distinguishes similar characters
- has generous x-height
- works across iOS and Android
- supports future languages
- is commercially practical

## Type rules

- Sentence case
- Left-aligned body copy
- Short line lengths
- Generous line height
- No all-caps body text
- No light weights for essential text
- Support dynamic text

## Type scale — corrected after on-device review

**Found too large and clunky on first build.** Only two things should read as large: screen titles (e.g. "Going quiet," "Reconnect" on Home) and primary action buttons. Everything else — body copy, input boxes, option labels, secondary text — should sit closer to the compact, dense scale used in Instagram and Gmail, not scaled up to match the titles.

- **Large (titles, primary buttons only):** the Home screen's circle header ("Going quiet"/"Reconnect"), and the main action button per screen.
- **Compact (everything else):** body paragraphs, message text boxes, option list labels and their descriptions, input fields, secondary buttons. This should visually read closer to a standard iOS system font size (roughly 15–17pt equivalent) than the larger, heavier weight currently used throughout — compare directly against Instagram or Gmail's own text sizing as the target density, not against Hold's current build.

This applies globally across the app, not just specific screens flagged in review — the whole component library (option cards, message boxes, buttons other than the two primary ones) should be audited against this, not patched screen by screen.

**Padding and spacing must shrink proportionally with the text, not just the font size.** Option cards (e.g. the Going Quiet reason cards, the Personalise starting-point selector) currently carry generous internal padding sized for the larger text. If only the font shrinks and the box padding stays as-is, the result is small text floating in an oversized container — a mismatch that can look worse than the original, not better. Reduce container padding, vertical spacing between stacked options, and card height together with the text, so the whole component feels proportionate at the new scale, not just the words inside it.
