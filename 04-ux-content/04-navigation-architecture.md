# Navigation architecture

No file previously described how the app is structured outside the linear Going Quiet → Taking Time → Reconnect journey. This fills that gap.

## Guiding principle

The main journey is sacred. When someone opens Hold while unwell, they shouldn't have to think about Library, History or Settings — they should see one clear action. Supporting tools stay accessible, but never in the way.

## Bottom navigation

- **Home** — the journey. Opens wherever the user left off (Normal, Taking Time, or Post-Reconnect state — see `04-ux-content/01-core-journeys.md`).
- **Library** — always available, independent of the Going Quiet journey. Someone can open Hold because they have one message they can't face replying to, with no need to have gone quiet first. Named "Library" rather than "Conversations" specifically to avoid the tab reading as a standing to-do list — a persistent nav item called "Conversations" can imply unfinished business just by convention, even with no badges or counts. The screen itself still leads with the Conversations reply-help experience (per-person, paste a message, get help wording a reply) rather than the template shelf, so the calmer name doesn't cost discoverability of the actual function — see "Library screen structure" below. Never shows an unread count or notification badge on its nav icon (see "No badges, no counts" below).
- **History** — reflective, not active. A timeline of previous quiet periods, one card per period. Patterns sits inside History via a segmented control at the top (History | Patterns) rather than a separate tab — see `03-product/04-patterns.md` for the full structure and free/Hold+ split.

## Settings (top-right icon, not a bottom tab)

Interaction: tapping the icon slides a panel out from the right edge of the screen (Gmail's slide-out drawer pattern, mirrored to the right rather than the left) rather than pushing to a new full screen — keeps context of where the user was.

Icon choice: a "hamburger" (☰, three lines) rather than a gear — visually cleaner and consistent with the reference screenshots reviewed. Either reads fine; hamburger was the preferred pick.

Contents: a settings panel with each item as its own row (see "Settings panel structure" below).

## Bottom navigation — icon and label pairing

Per the accessibility research in `02-research/04-accessibility.md`, use labelled icons, not icon-only — recognition (a familiar icon plus a short word) requires less cognitive effort than interpreting an unlabelled icon or reading text alone, which matters more than usual given who's using Hold and when.

Suggested icons (simple, filled or line-consistent with the rest of the design system, no colour-only meaning):

| Destination | Suggested icon | Label |
|---|---|---|
| Home | Hold's own circle mark (the same shape as the main interaction circle), not a literal house glyph — see "Home naming and icon" below | Home |
| Library | Speech bubble outline (no notification dot — see "No badges, no counts" below) | Library |
| History | A soft clock or gentle looping-path icon (avoid a plain "back in time" arrow, which can read as undo/error) | History |

Match Instagram's reference sizing for icon and label: compact, legible, not oversized — the icons in the reviewed screenshots are a reasonable target for scale and weight.

**Label length note:** superseded now that the tab is named "Library" (7 characters) rather than "Conversations" — no longer the longest label, no wrap/scaling concern. Kept here as history: the word "Conversations" itself wasn't wrong as a concept (it's still the name of the reply-help feature inside Library), it just carried unwanted task-list weight as a persistent nav label specifically.

## Selected-state ring for Circle pills

**Corrected:** this applies to pills, not avatar thumbnails. When a Circle pill is selected, use a soft white glowing ring around its edge — the same visual idea as Instagram's story ring, in white/glow rather than a coloured gradient — as an option alongside (or in place of) the existing dark-green-border approach from `05-design-system/02-colour-and-typography.md`, whichever reads more clearly against the pill's fill colour in practice.

## Circle shape: true circle by default, pill when the label needs more room

**Supersedes the earlier "Decided: pills" rule directly below (kept struck through for the record, not deleted, since the reasoning is still worth having on file).** True circles are Hold's actual core visual motif — a pill was the earlier fallback specifically because variable-length Circle names didn't fit a fixed circle legibly. The new rule keeps that reasoning but resolves it per-Circle instead of abandoning the circle shape for everyone:

- **One fixed diameter for every chip in the row — not grow-to-fit per label.** An earlier version of this rule let the circle's diameter grow to fit each label individually (floored at the accessibility minimum, capped short of an oversized blob); revised again after that produced a visibly inconsistent row, different chips reading at different heights. `STANDARD_CHIP_DIAMETER` is one constant, kept platform-specific by design, not reconciled into one shared number. Originally set at the bare platform accessibility minimum (44pt HIG / 48dp Material) after checking git history against the original pill component's own 38pt height; increased to 64pt/68dp (2026-08-10) for a more comfortable "story-circle" scale; increased again to **72pt on iOS, 76dp on Android** (2026-08-11, direct instruction, chosen option, a final figure given directly rather than measured) so Going Quiet's and Manage Circles' chips have room for a dropdown arrow (below) and still fit as true circles for common short names. Both increases are stylistic, well above the accessible tap-target floor either way, not accessibility fixes. A pill's own horizontal padding stays separate from the (still tight) padding budget the circle-fit check itself uses, so short labels can still plausibly become circles.
- **Dropdown arrow, appended into the measured label** (2026-08-11) — every selectable named-Circle chip (not "All," not "+") shows `" ▼"` collapsed / `" ▲"` expanded, using the same technique Manage Circles' own chip picker already had; Going Quiet's picker was missing this and now matches. A sent-and-collapsed chip shows its existing checkmark look instead, no arrow — the two signals (sent vs. expandable) don't stack. Appending the arrow into the same measured-text-width check the circle-vs-pill decision already uses means longer names need more room to stay circles, which is the direct reason for the diameter increase above — not a coincidence.
- **Sizing rule, not a character-count threshold:** measure the Circle name's actual rendered text width at the user's current font size (Dynamic Type / font-scale respected live, re-measured on change) against `STANDARD_CHIP_DIAMETER`. If it fits inside as a circle, render a true circle at exactly that fixed diameter — same size regardless of which short label it is. If it doesn't, fall back to the stadium-pill shape at the *same fixed height*, only the width growing to fit the text — literally the same circle, stretched wider, not a separately-sized shape. Height itself does not vary by label or grow with font size; at very large accessibility text sizes a label could theoretically need more vertical room than the fixed height provides, which is an accepted trade-off of keeping the row visually consistent, not an oversight.
- Selected-state ring and the row's partial-cutoff scroll cue work identically on either shape — both are the same corner-radius formula (height ÷ 2), just at different widths.
- Implemented as one shared, isolated component (`AdaptiveCircleChip`) rather than per-screen shape logic, so this can't drift between screens the way pill styling once could — this includes icon-only chips like Going Quiet's "+" (New Circle) button, which was found to still be hand-styled separately outside the shared component and was brought in properly rather than patched again.
- **Press feedback (a uniform darken on tap) lives in the shared component itself**, not per call site — a real gap once, when "+" briefly lost its own press effect moving onto the shared component without one.
- **Selection and sent-state are two independent flags, not one** — `isSelected` (part of the current compose action) and `hasSentThisSession` (already sent this session, whatever "this session" scopes to for that flow: the still-open Hold period for Going Quiet and Taking Time's update, a durable reconnecting-period marker for Reconnect, per-person completion state for Conversations' Quick message). Priority: selected wins regardless of sent; else sent shows the softened/desaturated look with no ring; else default. Sent is never cleared by deselecting — only a genuine send changes it — so reselecting an already-sent Circle to send again, then deselecting without sending, correctly returns to the sent look rather than default. Now true everywhere a Circle can be selected — every Circle-picker row in the app is on `AdaptiveCircleChip`.

~~**Decided: pills**, specifically fully rounded/stadium-shaped pills (rounded ends, not just rounded corners) with generous horizontal padding, not rectangular chips. Circles are Hold's core visual motif and read as calmer in the abstract, but Circle names vary in length ("Close" vs "Book Club" vs longer custom names), and cramming variable-length text into a fixed circle forces either tiny type or truncation — both read as *less* calm than a well-padded pill, not more. A generously rounded pill keeps most of the circle's softness while staying legible at any name length.~~

## Circle picker layout — single scrollable row

**Decided:** Circle pills sit in one horizontal row, scrollable left when there are more than fit on screen, rather than wrapping onto multiple rows. This scales cleanly now that Circles are unlimited on Free — a wrapped grid gets visually messy fast once someone has several Circles; a single scrollable row stays clean regardless of count.

Selected pills carry a down-arrow to expand into a recipient box beneath the row — see the "Who needs to know?" step in `04-ux-content/01-core-journeys.md` for the full interaction, which deliberately mirrors Conversations' Tier 2 → Tier 3 dropdown so both screens share one expand-a-Circle pattern rather than two different mechanisms.

- Close stays first in the row and keeps its stronger fill/priority position, as already decided.
- **Revised again — "+ New Circle" is pinned outside the scrollable row entirely, always visible; "All" is the scrollable row's first item, not pinned alongside "+".** "+" sits fixed at the row's start; the scroll begins with "All," then the named-Circle pills. "All" doesn't need to persist once someone's scrolled past it the way "+" does, since it's only relevant before scrolling starts. This supersedes the immediately-prior "+ pinned inside the row, right after All" placement. Your Circles (Settings) still uses the separate heading-level "+" icon-button pattern instead, since it has its own title/header bar that Going Quiet's inline "Who needs to know?" step doesn't.
- Where content extends beyond the visible row, the last visible pill should be **partially cut off at the edge**, not a hard stop — a visible cue that more exists to scroll to, rather than the row appearing to simply end.
- "Manage your Circles" stays a separate line beneath the picker, unaffected by this layout change.

## Home naming and icon

Label stays **"Home"** even though the content underneath changes by state (Normal / Taking Time / Post-Reconnect) — nav labels name the destination the user returns to, not the momentary state, and "a stable place to come back to whatever state you're in" fits Hold's ethos rather than contradicting it.

The **icon** is what should change: not a literal house glyph, which is a generic pictogram unrelated to anything else in the app. Use Hold's own circle mark — the same shape as the main interaction circle — as the Home tab icon instead. This ties the nav bar back to the one shape that already carries the app's meaning (see `05-design-system/01-design-direction.md`) rather than introducing an unrelated symbol just for the tab bar.

## Settings panel structure

**Corrected:** not a single About screen with headed sub-sections — the hamburger opens a panel where each item is its own row, tapped through to its own screen. "Our Mission" (renamed from the generic "About") is one row among several, not the container for the others.

**Panel order, grouped by purpose rather than one flat list — revised from the original Mission-first order** (see `08-decisions/01-decision-log.md`): someone opening this menu while unwell is usually here to do something practical, not to read about the app's values, so task-oriented content leads and browsing/values content follows. Groups are separated by spacing alone, with no visible heading text — only the final group gets a divider line above it, since it's genuinely lower-priority legal/data reference rather than daily-use items.

**Manage Hold**

1. **Your Circles**
2. **Notifications**
3. **Language**
4. **Connected Accounts**

**About Hold**

5. **Our Mission** — values and privacy-values messaging in Hold's own voice, including the fuller version of "no one should be judged by their illness or its limitations"
6. **Research** — the evidence base behind Hold's design and safety approach (accessibility research, safeguarding evidence, icon/label findings, and the lived-experience guilt-spiral/supportive-language research that shaped Hold's voice — see `02-research/`), surfaced honestly rather than left as internal documentation only. Can state plainly that Hold looked to the lived experience of people who deal with the guilt spiral when designing how it speaks: gentle, short, genuine statements that validate; permission without pressure or commentary.
7. **Hold+** — see "Hold+ visibility" below for its other access point (Patterns' contextual surfacing)

**Support**

8. **Feedback**
9. **Share Hold** — invite someone else to Hold

— divider line above this group only, since it's lower-priority legal/data reference rather than daily-use items —

**Legal and data**

10. **Privacy Policy** (link)
11. **Terms** (link)
12. **Delete my data** — wipes every saved Circle, Hold history entry, in-progress reply, Conversations list, saved template, message draft, and remembered AI-drafting detail (including turning the AI memory toggle back off, not just clearing what it had captured) from the device, plus the anonymous AI-proxy install id (a fresh one is generated on next use, same as a genuine fresh install). Deliberately content-only: the one-time seen-welcome-screen/seen-retention-note flags are left alone, so a wipe doesn't force someone back through onboarding — see `08-decisions/04-open-questions.md`, "'Reset app' as a distinct action from 'Delete my data.'" Not part of the original panel spec, added here since it needed a home somewhere reachable

**Spacing intent between groups:** Feedback/Share and Legal and data move together as one bottom-anchored block, pinned to the panel's bottom edge (mirroring the top padding above Your Circles) rather than trailing at a fixed distance below About Hold. The single largest gap in the panel sits above that whole block — the one real section break, between values/browsing content (Manage Hold, About Hold) and the practical, occasional-use rows below (Feedback/Share, then the divider, then Legal and data). None of the group spacing relies on a visible heading label, only breathing room (and, for the last group only, the divider line itself) to read as distinct sections.

**No icons in the drawer, deliberately, for now.** Considered and deferred rather than omitted by default — the same icon-plus-label accessibility reasoning used for the three bottom-nav tabs (`02-research/04-accessibility.md`: a familiar icon plus a short word lowers recognition effort versus text alone) would apply here too, but a dozen rows each needing a distinct, legible glyph is a meaningfully bigger design task than three tab icons, and plain text rows are already fully clear on their own. Worth revisiting once the drawer's contents settle, not a closed door.

**"Delete my data" uses a darker, muted red**, not the same red used for Circle-deletion/Hold-history confirms at their usual size and weight — the same destructive signal (this is the one truly irreversible action in the drawer) toned down for a passive row label sitting among plain-text rows, rather than an active confirm button, so it doesn't read as more alarming than the rest of the calm panel around it. See `05-design-system/02-colour-and-typography.md` for the derivation.

Bottom nav stays at three items — Home, Library, History. Settings deliberately does not become a fourth bottom tab, even though some reference apps (e.g. Balance) use an Account tab. Circles were already moved out of the bottom nav specifically because they're occasional maintenance rather than a reason someone opens the app; Settings sits in that same category, so it stays behind the corner icon rather than gaining equal billing with Home, Library and History.

## Hold+ visibility

**Revised: no persistent top-bar element.** A standing visual element in the top bar — even styled quietly — reads as ongoing pressure/visual noise, inconsistent with Hold's "held, not managed" tone. Supersedes the earlier two-access-point wording (see `08-decisions/01-decision-log.md`).

Two access points instead, both reaching the same destination:

- The Settings drawer's Hold+ row (above).
- Contextual surfacing at natural moments — currently the Patterns screen's "More with Hold+" section, shown below the free stats as an additive invitation ("here's more depth if it'd help you"), never a locked or greyed-out preview — see `03-product/04-patterns.md`.

Both now route to a concrete destination, `app/settings/hold-plus.tsx`: an honest info screen built from `07-business/02-pricing-principles.md`'s real content (free tier, what Hold+ would add, Founding Member pricing, fair-access commitments), closing with a plain "not open for purchase yet" note rather than a working purchase flow, since no entitlement/billing system exists yet.

- Never a banner, modal, or interruption to the core journey (already established in `07-business/02-pricing-principles.md`).
- Never framed as urgency or a countdown — an invitation, not a wall.

## Circle setup

Circles are set up inline, during first use, as part of the natural Going Quiet flow — not as separate onboarding, so it doesn't feel like labour. "+ New Circle" and "Manage your Circles" are available directly from the Going Quiet screen. Ongoing management (editing, deleting, reorganising) lives in Settings.

## Library screen structure

**Revised:** the bottom-nav tab is called Library, not Conversations — but the screen itself leads with the Conversations reply-help experience, not the template shelf, so renaming the tab doesn't cost discoverability:

1. **Conversations** (primary, top of screen) — the per-person reply-help experience: paste in a message someone sent, get help wording a reply, tick/untick people as complete. This is what most people are actually there for, and it's what they see first.
2. **Templates** (secondary section, below) — saved messages (Messages / Emails / OOO / Social), built up over time via the "Save as template?" prompt, not present during onboarding.

Templates build up naturally over time: whenever the user edits an AI draft or writes their own message, Hold asks "Save as template?" — an explicit, opt-in prompt, not automatic capture. Over months this makes the section genuinely personalised without ever silently harvesting what someone writes.

**Template/chip explanations live here, not in the live composition flow.** The Going Quiet chip suggestions (e.g. "unwell," "overwhelmed," "need time") are deliberately compact and unexplained in the moment, to keep composition fast for someone who already knows what they mean. The fuller explanation of what choosing a given template actually communicates (matching the description text the original option cards used to carry, e.g. "Say your capacity is lower than usual") lives in Library instead — somewhere to look something up occasionally, not something repeated every time someone goes quiet. This resolves the trade-off of moving from descriptive cards to compact chips: the context isn't lost, it just moves to where it's actually useful rather than adding friction to the fast path.

A user opens Library because they need help communicating; Conversations is what they find immediately, Templates is what supports that once they're there.

## The Transition screen

ChatGPT-side proposal: a brief screen between Going Quiet and Taking Time, with quiet, non-cheerful reassurance copy ("You've taken the first step... Taking time to recover isn't selfish. You don't need to earn rest.") before "Begin Taking Time."

**Not yet decided** whether this becomes part of the actual navigation flow (i.e. Going Quiet → Transition → Taking Time, a genuine extra screen) or stays a copy idea folded into the existing Going Quiet completion state. Tracked here rather than in `04-ux-content/01-core-journeys.md` because it's fundamentally a navigation-structure question (does the journey get a new screen or not), not just a wording one.

## No badges, no counts

Library never shows an unread count or notification badge on its nav icon. Reassurance in the Conversations section must stay opt-in — the person chooses to look, rather than the app creating ambient pressure every time they open Hold.
