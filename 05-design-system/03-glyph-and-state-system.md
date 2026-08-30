# Glyph and state system

**Status:** Spec, not built. From an extended external design/research session (2026-08-19 onward), handed to this repo 2026-08-31. See `08-decisions/01-decision-log.md`, 2026-08-31.

**Flagged before anything else in this file: relationship to existing marks not yet reconciled.** This repo already has two established visual assets that may or may not be the same thing this spec calls for — checked directly, not assumed compatible:
- `HoldMark` (`hold-app`'s own component name) — referred to in `04-ux-content/04-navigation-architecture.md` as "the logo," shown above the three-line message sequence on completion/transition screens.
- The bottom-nav tab icon, described in `08-decisions/01-decision-log.md` (2026-07 row) as "Hold's own circle mark, not a literal house glyph."

Neither of those is documented anywhere as a *state* glyph (i.e. something whose position/shape changes to represent On Hold / Reconnecting / etc.) — both read, from their existing descriptions, as static brand marks. This spec calls for a single glyph that changes position to represent state. Before this is built, confirm whether the state glyph described below **is** a state-bearing version of the existing circle mark/HoldMark (most likely, given both are already circle-based), or a genuinely separate third asset — this file assumes the former is more likely but does not decide it.

## One universal glyph — not multiple icons for different causes

**Decided:** a single, stable outward-facing glyph representing only one meaning: *ordinary response expectations are paused.* Do not build visibly different icons for overwhelm, illness, protective withdrawal, conflict, grief, restorative solitude, or crisis. Multiple public symbols would disclose sensitive information by their type alone, force recipients to decode a taxonomy, create implicit status hierarchies, and — critically — make a protective Hold identifiable to an unsafe person specifically because of which icon was used. One glyph, always. This is a direct extension of the reconnection-must-never-be-compulsory requirement (`06-privacy-security/07-reconnection-safety-requirements.md`): a glyph that leaked *why* would violate the same "undiscoverable by the other party" principle a status label would.

**Direction: a dot resting inside an open circle.**
- The dot represents the person / their available capacity.
- The circle represents a protected boundary or held space — open, not closed, so it never implies imprisonment.
- The dot's position within the circle conveys state.

**Rejected alternatives, logged so they aren't re-proposed without reason:** two facing arcs (risk: reads as brackets/quotation marks/corporate logo), a horizon/resting sun (risk: implies a predictable, guaranteed return), a seed in a circle (risk: too detailed at small sizes, implies growth as an obligation), a pause mark in a circle (risk: reads as media-player iconography, implies automatic resumption).

## State variations — position/shape, never colour or motion alone

| State | Dot position |
|---|---|
| Available | Centred within the open ring |
| On Hold | Resting low, at the bottom of the ring |
| Update available | A small pulse appearing outside the ring |
| Reconnecting | Rising slightly from the bottom |
| Open/fully returned | Moved toward the ring's opening |

**Hard accessibility requirement:** every state must be distinguishable by its static position alone, without relying on colour or on seeing the transition animation — a direct extension of the existing colour-blindness/non-colour-based differentiation rule already standing for the rest of the app (see the "✓" prefix convention used elsewhere for exactly this reason).

## Contrast and touch target

**Contrast:** the glyph is a "meaningful graphic" under the app's existing colour requirements (`02-colour-and-typography.md`), so it must meet at least 3:1 contrast against its background in every state, across all four existing palette combinations (light-normal, light-quiet, dark-normal, dark-quiet) — checked separately per palette, the same way the four-palette token system was checked for the rest of the app, not just once in a default theme.

**Touch target:** everywhere the glyph is tappable within the app (not the web page — see `04-ux-content/07-universal-web-page.md` for its own independent requirement), it must meet the platform-standard minimum touch target size (44×44pt iOS / 48×48dp Android) regardless of how small the glyph renders visually at 16–24px — pad the tappable area, don't shrink it to match the visual glyph size.

## Reduced motion

Because meaning lives in the dot's *resting position*, not in the motion between positions, a reduced-motion mode is not a redesign — it's simply skipping the transition animation and rendering the new resting position directly.

**Implementation requirement:** every glyph state change must have (a) a full animated transition for standard use, and (b) an instant, static equivalent for `prefers-reduced-motion`/system reduced-motion setting, showing only the before/after resting positions with no intermediate motion. Both must be built together, not the static version added later as a follow-up — matching the app's own existing "Reduce Motion sweep" precedent (`04-navigation-architecture.md`).

## Learning period

A new symbol needs time to acquire shared meaning. For at least the first phase after launch, the glyph should not be sent alone — pair it with a short explanation on first exposure:

> "◉ On Hold — responses aren't expected right now. This isn't automatically about the relationship."

Accessibility text describing the glyph's meaning must always be available (screen-reader label, alt text, tooltip/long-press), not phased out once the symbol is assumed to be "known" — some recipients will always be encountering it for the first time.

## Anti-compulsive-checking requirement

**The risk:** any persistent, checkable status indicator can itself become something a waiting person compulsively re-checks — the same intermittent-reward mechanic that makes notification-checking habitual in the first place. A glyph that solves "ambiguous silence" could inadvertently create a new, smaller version of the exact anxious-monitoring behaviour Hold exists to reduce, just relocated from message-checking to glyph-checking.

**Mandatory design constraints to prevent this:**
- No visible "last updated" or "last changed" timestamp on the glyph itself.
- No push notification to recipients when a glyph state changes, unless the Hold user has explicitly chosen to send an update.
- No feature that rewards or gamifies checking (no streak, no "you were the first to see this," nothing that makes repeat-visiting the glyph feel productive) — consistent with the app's own standing "no badges, no counts, no streaks" rule (`04-navigation-architecture.md`).
- The glyph's home on the universal web page (`04-ux-content/07-universal-web-page.md`) should not auto-refresh or show real-time state; state should update only on a fresh page load a person deliberately initiates.

## Technical constraints

The glyph must work:
- At 16–24px, in monochrome.
- Beside a name, in a status bar, and embedded in shared text/links on third-party platforms (WhatsApp, iMessage, etc.) — verify rendering doesn't degrade to an ambiguous shape at the smallest sizes third-party platforms might display it at.
- Without resembling medical/danger iconography, a "blocked" symbol, or a media-player pause/play control.

## Research panel candidate — Settings → Research

> "Hold uses one symbol, not several, on purpose — different icons for different reasons would reveal more than most people want to share, and could even make it identifiable to someone unsafe. One meaning, always: your reply expectations are paused."

## Status

Not built in `hold-app` yet. Blocked on the HoldMark/circle-mark reconciliation question flagged at the top of this file before implementation begins.
