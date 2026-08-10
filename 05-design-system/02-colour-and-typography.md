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
| Strong/primary green fill | Primary or most important item (e.g. Close) |
| Soft sage fill | Standard selectable item |
| Dark green border | Selected (must not rely on fill/colour change alone — pair with a checkmark or equivalent) |
| White/outlined pill | Secondary navigation, add or manage action (e.g. "+ New Circle," "Manage your Circles") |

Keep the palette restrained — primary fill, soft fill, border, outline is enough vocabulary; adding more shades of green reduces clarity rather than adding it.

## Destructive/error colour in a passive label context

The app's error/destructive red is used for active confirm actions (Circle deletion, Hold history entry deletion) at their usual size and weight. Applied to a passive row label sitting among plain-text rows — the Settings drawer's "Delete my data" — the same hex read as more alarming than intended, simply by being the only coloured text in an otherwise calm, monochrome list. Resolved by deriving a darker, calmer shade from the existing token rather than inventing a new one: the error colour blended roughly 85/15 toward the body text colour (an initial 70/30 blend on-device read as too close to brown/grey — barely red — so the ratio was lightened back up). Still clearly identifiable as red at a glance (never drifts toward the app's cool green/sage palette, which would blur the destructive signal), just toned down enough to sit quietly until actually needed.

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

- **Large (titles, primary buttons only):** the Home screen's circle header ("Going quiet"/"Reconnect"/"Taking time"), and the main action button per screen. "Taking time" specifically was corrected back up to this tier (2026-08-10) after reading as too small/tucked-away for a state that's meant to read as a deliberate, held state, not an incidental label — see the decision log for why this reopens the ~17pt figure decision 136 set for it.
- **Compact (everything else):** body paragraphs, message text boxes, option list labels and their descriptions, input fields, secondary buttons. This should visually read closer to a standard iOS system font size (roughly 15–17pt equivalent) than the larger, heavier weight currently used throughout — compare directly against Instagram or Gmail's own text sizing as the target density, not against Hold's current build.

This applies globally across the app, not just specific screens flagged in review — the whole component library (option cards, message boxes, buttons other than the two primary ones) should be audited against this, not patched screen by screen.

**Padding and spacing must shrink proportionally with the text, not just the font size.** Option cards (e.g. the Going Quiet reason cards, the Personalise starting-point selector) currently carry generous internal padding sized for the larger text. If only the font shrinks and the box padding stays as-is, the result is small text floating in an oversized container — a mismatch that can look worse than the original, not better. Reduce container padding, vertical spacing between stacked options, and card height together with the text, so the whole component feels proportionate at the new scale, not just the words inside it.

## Button patterns — two categories, not one shared style

The app's action buttons split into two deliberately different shapes, not a single "primary button" style used everywhere. Getting this categorisation wrong (styling a repeated action as a one-time one, or vice versa) reads as a mismatch, so a button's *category* — how often it's tapped in one sitting — decides its shape, not how visually important it feels.

**One-time completion action** — ends or advances a whole flow, tapped once per visit (e.g. Reconnect's final "Done," "Begin Taking Time," "Get started"). Full-width-feeling, prominent: the existing **Strong/primary green fill** token (above) + white text, a full pill radius (`theme.radius.pill`, matching every other "strong"/filled element in the app rather than the smaller rounded-rectangle radius this used before, which read as dated next to everything else), and real side margins rather than spanning edge-to-edge of its own already-padded container. Text label only, deliberately no icon — see "Begin Taking Time," below.

**Repeated/per-item action** — select a circle or person, tap Send, repeat, several times in one sitting (Going Quiet's per-Circle Send, Reconnect, Taking Time's "Send an update," Conversations' Quick message and Personalise). Compact and icon-only: a standard paper-plane send glyph (not a custom icon — legibility and instant recognition over novelty), filled in the same Strong/primary green as the one-time button so it still reads as "the affirmative action," but a small circle rather than a full-width bar — a different, smaller shape entirely, not a smaller version of the completion button. Icon-only means the button carries no visible label, so `accessibilityLabel="Send"` (or a more specific variant, e.g. "Send to Book Club") does the work a text label would otherwise do. Still meets the bare 44pt (iOS) / 48pt (Android) platform accessible tap-target floor, regardless of how compact the icon reads visually — deliberately smaller than the Circle chips, which grew past that same floor (2026-08-10) to a more comfortable stylistic size; the two are no longer the same number by design, not an inconsistency. **Exception — Quick message's per-Circle bulk Send:** shows a visible `"Send (N people)"` label beside the icon instead of staying icon-only, since how many people a send reaches is useful, neutral, confirmatory information worth showing on-screen (this is not the kind of elapsed-time/pressure count the app's "no counts" rule guards against). Says "people," not "Circles" — this button always sends within exactly one Circle, so a per-Circle count would misdescribe what it does.

**"Begin Taking Time" specifically stays icon-free, by deliberate decision, not an oversight.** This is the app's one restful completion moment, not an achievement — an icon here (a filled circle, a moon) would collide with symbols already meaningful elsewhere (Circle iconography, the moon-cycle overlay feature) and add action-energy to a screen built to feel calm, not accomplishment-driven. Every other one-time completion button follows the same text-only rule.
