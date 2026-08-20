# Navigation architecture

No file previously described how the app is structured outside the linear Going Quiet → Taking Time → Reconnect journey. This fills that gap.

## Guiding principle

The main journey is sacred. When someone opens Hold while unwell, they shouldn't have to think about Library, History or Settings — they should see one clear action. Supporting tools stay accessible, but never in the way.

## Bottom navigation

- **Home** — the journey. Opens wherever the user left off (Normal, Taking Time, or Post-Reconnect state — see `04-ux-content/01-core-journeys.md`).
- **Library** — always available, independent of the Going Quiet journey. Someone can open Hold because they have one message they can't face replying to, with no need to have gone quiet first. Named "Library" rather than "Conversations" specifically to avoid the tab reading as a standing to-do list — a persistent nav item called "Conversations" can imply unfinished business just by convention, even with no badges or counts. The screen itself still leads with the Conversations reply-help experience (per-person, paste a message, get help wording a reply) rather than the template shelf, so the calmer name doesn't cost discoverability of the actual function — see "Library screen structure" below. Never shows an unread count or notification badge on its nav icon (see "No badges, no counts" below).
- **History** — reflective, not active. A timeline of previous quiet periods, one card per period. Patterns sits inside History via a segmented control at the top (History | Patterns) rather than a separate tab — see `03-product/04-patterns.md` for the full structure and free/Hold+ split.

### Bottom nav visibility — two-tier rule, 2026-08-13 (supersedes the composition-everywhere rule below)

**Screen category decides first, composition state second, replacing the earlier same-day "hides while composing, anywhere" rule.** Tier 1 — Going Quiet, Transition screens, Reconnect (including its resumed "Finish Reconnecting" state) — hides the nav bar throughout, no exceptions, matching the same accidental-navigation-away protection the composition-based rule was originally built for. Tier 2 — Home, Library, History/Patterns, Settings and its sub-screens — shows the nav bar by default, hiding only while a docked text-composition field is actively focused *within that tier*.

This deliberately includes Settings, which the tab-group-vs-stack-screen split below couldn't reach under the old architecture at all (Settings screens are pushed root-stack screens, not tab-group children) — the nav bar is now a root-level overlay rather than the Tabs navigator's own bar, specifically so it can show there too.

**Swipe-back (`gestureEnabled`), resolved 2026-08-13: unconditional on Going Quiet and Reconnect, not composition-gated.** Now that the nav bar's own Tier 1 rule is "hidden throughout, no exceptions," an inconsistent swipe-back (only disabled while actively composing) would undercut that same accidental-exit protection — both screens now set `gestureEnabled: false` statically, matching the four already-static completion/transition screens (`welcome`, `create/done`, `return/transition`, `return/done`) rather than the composition-driven rule below. **The explicit Back button is untouched** — only the gestural swipe path is removed; a deliberate tap on Back remains available exactly as before.

### Bottom nav visibility during active composition (superseded for both the nav bar and swipe-back on Going Quiet/Reconnect — Library only, now), 2026-08-13

**Rule: the bottom nav bar hides whenever a docked text-composition field is actively focused, anywhere, and shows in every other state** — driven by "is a text input currently focused?" rather than a hand-maintained per-screen list, so it extends correctly to any future screen without a fresh decision each time. Closes a second, easily-missed path to the same in-progress-message data-loss risk already addressed by disabling the swipe-back gesture during composition — an accidental tap on the nav bar mid-message is just as capable of losing work as an accidental swipe; the explicit Back/close control remains the deliberate way to leave either way. Built as one shared mechanism with the swipe-back disable, not two separately-maintained ones, per direct instruction.

In practice, given how the app's screens are actually split between the tab group and pushed stack screens: Going Quiet and Reconnect are stack screens outside the bottom-tab group entirely, so the nav bar was never rendered there regardless — only the swipe-back half of the rule did anything for them, and even that's since become unconditional (see above), so this composition-driven rule now only actually governs Library. Home and History have no composition concept, so neither needed anything. Research is not part of Library and never has been — see "Library screen structure" below — so, like Going Quiet/Reconnect, it has no tab bar to hide in the first place.

### Bottom nav bar surface, 2026-08-13

The pill is the only shape on screen — there is no separate background container behind it; it floats directly over whatever screen content sits beneath. The pill's own fill is a frosted-glass surface (blur + a translucent tint of the active palette's `surfaceStrong`), not a flat colour, and follows whichever palette Home is currently resting in (normal vs. quiet/Taking Time) rather than always using the normal palette — so it never visibly clashes with a quiet-palette screen behind it.

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

- **One fixed diameter for every chip in the row — not grow-to-fit per label.** An earlier version of this rule let the circle's diameter grow to fit each label individually (floored at the accessibility minimum, capped short of an oversized blob); revised again after that produced a visibly inconsistent row, different chips reading at different heights. `STANDARD_CHIP_DIAMETER` is one constant, kept platform-specific by design, not reconciled into one shared number. Originally set at the bare platform accessibility minimum (44pt HIG / 48dp Material) after checking git history against the original pill component's own 38pt height; increased to 64pt/68dp (2026-08-10) for a more comfortable "story-circle" scale; increased to 72pt/76dp (2026-08-11) for a dropdown arrow that has since moved out of this measurement entirely (below); increased a fourth time to **90pt on iOS, 95dp on Android** (2026-08-11, later same day, direct instruction, final figure given directly rather than measured) — Circles are core to how the app is used, and the previous size left little margin for the longest common label. Every increase has been stylistic, well above the accessible tap-target floor either way, not an accessibility fix. A pill's own horizontal padding stays separate from the (still tight) padding budget the circle-fit check itself uses, so short labels can still plausibly become circles. Estimated (not device-rendered) text-width check against the 90pt/95dp diameter: "Close," "Friends," "Work," "All," and typical short user-created names fit as true circles at default text size; "Book Club" (9 characters) sits right at the boundary, a genuine close call not confidently resolved either way; longer custom names render as pills, as designed. At the largest Dynamic Type accessibility size, essentially every name — including "Close" and "All" — becomes a pill; this is the intended degradation, not a bug, and no label is ever shrunk or truncated at any size (single-line text against an unconstrained pill width, inside a chip height taller than even the largest accessibility line height).
- **Dropdown arrow is its own independent tap target, not appended into the label** (2026-08-11, corrects the same-day entry directly below/above in the decision log) — every selectable named-Circle chip (not "All," not "+") now renders as two separate elements: the circle itself (tapping it selects/deselects for sending, unchanged meaning) and a small separate arrow (tapping it opens/closes that Circle's member list independently, without affecting selection at all). Tapping one never changes the other's appearance or state. This is why the diameter above no longer needs to budget room for the arrow glyph — it only has to fit the Circle name itself. **Position corrected the same day, later:** the arrow first shipped floating beside the circle, which on-device read as ambiguous about which circle it belonged to; moved to sit inside the circle's own boundary instead, toward its right edge, with a small scrim badge behind the glyph for visual separation from the label underneath it — still independently tappable, just contained within the chip's shape rather than floating outside it. **Regression, found and fixed later the same day:** a subsequent redesign pass removed the arrow entirely along with the reselect machinery it used to sit inside — its own purpose (viewing/adjusting a Circle's members on demand) turned out to still be needed independent of that machinery, so it was restored, now single-expand only (only one Circle's member list open at a time, opening a second closes the first) — see `01-core-journeys.md`'s Going Quiet section, point 2. **Position corrected a third time (2026-08-11):** the restored version still visually overlapped the (also-centred) label text, since its tap target stretched the chip's full height and centred within it, landing at the exact same vertical position as the label. Anchored to the bottom of the chip instead, no full-height stretch; growing the circle again to make more room was considered and rejected in favour of repositioning, since the diameter had already grown four times this same day for other reasons.
- **"All" is a clean toggle over every Circle with contacts, and remembers what was selected before it was tapped.** Two real bugs found on-device the same day: an empty-Circle filter was silently dropped in a redesign pass (restored); and a genuine race condition in how a bulk "All" toggle was implemented as N sequential individual toggles, each reading a potentially-stale selection snapshot, made the actual result non-deterministic under rapid firing. Fixed structurally — one atomic selection-replace, not a loop — rather than patched. Deselecting "All" now restores the exact selection from before it was tapped, not a clear-to-empty (a deliberate divergence from Taking Time's own "Send an update" picker, which does just clear to empty — confirmed as wanted specifically for Going Quiet).
- **Reconnect's own sent-state chips, corrected:** the checkmark prefix (`"✓ Name"`) was found to be the actual cause of a chip visibly inflating into a pill shape and growing in size — the checkmark was baked into the measured label text itself, not a separate badge, so the circle-fit check could tip over for a long-enough name. Reconnect's own names (Circle names and individual people's names, often longer than Going Quiet's typical short Circle names) were the ones actually crossing that threshold. Fixed by dropping the checkmark there entirely — sent state is colour-only (the same dark-green fill used everywhere else), true circle shape preserved. The same underlying "✓ in the label" pattern is unchanged elsewhere (Going Quiet's own picker, Taking Time's "Send an update") — flagged as a latent risk for a sufficiently long Circle name, not fixed there since it isn't reported as broken.
- **Sizing rule, not a character-count threshold:** measure the Circle name's actual rendered text width at the user's current font size (Dynamic Type / font-scale respected live, re-measured on change) against `STANDARD_CHIP_DIAMETER`. If it fits inside as a circle, render a true circle at exactly that fixed diameter — same size regardless of which short label it is. If it doesn't, fall back to the stadium-pill shape at the *same fixed height*, only the width growing to fit the text — literally the same circle, stretched wider, not a separately-sized shape. Height itself does not vary by label or grow with font size; at very large accessibility text sizes a label could theoretically need more vertical room than the fixed height provides, which is an accepted trade-off of keeping the row visually consistent, not an oversight.
- Selected-state ring and the row's partial-cutoff scroll cue work identically on either shape — both are the same corner-radius formula (height ÷ 2), just at different widths.
- Implemented as one shared, isolated component (`AdaptiveCircleChip`) rather than per-screen shape logic, so this can't drift between screens the way pill styling once could — this includes icon-only chips like Going Quiet's "+" (New Circle) button, which was found to still be hand-styled separately outside the shared component and was brought in properly rather than patched again.
- **Press feedback (a uniform darken on tap) lives in the shared component itself**, not per call site — a real gap once, when "+" briefly lost its own press effect moving onto the shared component without one.
- **Selection and sent-state are two independent flags, not one** — `isSelected` (part of the current compose action) and `hasSentThisSession` (already sent this session, whatever "this session" scopes to for that flow: the still-open Hold period for Going Quiet and Taking Time's update, a durable reconnecting-period marker for Reconnect, per-person completion state for Conversations' Quick message). Priority: selected wins regardless of sent; else sent shows the softened/desaturated look with no ring; else default. Sent is never cleared by deselecting — only a genuine send changes it — so reselecting an already-sent Circle to send again, then deselecting without sending, correctly returns to the sent look rather than default. Now true everywhere a Circle can be selected — every Circle-picker row in the app is on `AdaptiveCircleChip`. A previously real bug in this same shared component — an outline chip like "+" could never show its selected ring at all, since the ring style was gated on "not outline" — was found and fixed (2026-08-11) as part of giving "+" its own active/open state (below).

~~**Decided: pills**, specifically fully rounded/stadium-shaped pills (rounded ends, not just rounded corners) with generous horizontal padding, not rectangular chips. Circles are Hold's core visual motif and read as calmer in the abstract, but Circle names vary in length ("Close" vs "Book Club" vs longer custom names), and cramming variable-length text into a fixed circle forces either tiny type or truncation — both read as *less* calm than a well-padded pill, not more. A generously rounded pill keeps most of the circle's softness while staying legible at any name length.~~

## Circle picker layout — single scrollable row

**Decided:** Circle pills sit in one horizontal row, scrollable left when there are more than fit on screen, rather than wrapping onto multiple rows. This scales cleanly now that Circles are unlimited on Free — a wrapped grid gets visually messy fast once someone has several Circles; a single scrollable row stays clean regardless of count.

Selected pills carry a down-arrow to expand into a recipient box beneath the row — see the "Who needs to know?" step in `04-ux-content/01-core-journeys.md` for the full interaction, which deliberately mirrors Conversations' Tier 2 → Tier 3 dropdown so both screens share one expand-a-Circle pattern rather than two different mechanisms.

- **Close stays first in the row (its priority position is unchanged), but no longer carries any colour distinctiveness (2026-08-11, corrects the "stronger fill" line of the 2026-07 decision this bullet used to restate)** — Close uses the exact same sage-default/dark-green-sent-fill treatment as every other Circle. Its only remaining secondary cue is a bolder font weight on its label; fixed-first position is the primary identification mechanism, deliberately not doubled up with a second colour-based signal.
- **Revised again — "+ New Circle" is pinned outside the scrollable row entirely, always visible; "All" is the scrollable row's first item, not pinned alongside "+".** "+" sits fixed at the row's start; the scroll begins with "All," then the named-Circle pills. "All" doesn't need to persist once someone's scrolled past it the way "+" does, since it's only relevant before scrolling starts. This supersedes the immediately-prior "+ pinned inside the row, right after All" placement. Your Circles (Settings) still uses the separate heading-level "+" icon-button pattern instead, since it has its own title/header bar that Going Quiet's inline "Who needs to know?" step doesn't.
- **Confirmed app-wide, 2026-08-13 — not a Going-Quiet-specific placement.** Every row of this kind ("+"-plus-"All"-plus-Circle-or-person-chips) follows the same pinned "+"/first "All" layout: Reconnect's own Circle-browsing row and its shared per-person pill row (each gets its own "+"/"All" pair — "+" adds a person to the audience in both, "All" scoped to the whole audience from the Circle row vs. only what's currently visible from the pill row), and Library/Conversations' own Circle-browsing row. Library's second row (expanded Circles' people, one shared list) has no "+"/"All" of its own and wasn't given one — it never had that concept, and adding one wasn't part of this correction. Your Circles (Settings) is unaffected, per the header-bar exception immediately above.
- **"+" final spec (2026-08-11):** the glyph alone, no baked-in text, sized noticeably larger/bolder than the small arrow glyph beside named chips (it has no competing label text sharing the circle). A "New Circle" caption sits beneath it, with a small deliberate gap, only while active — close enough to read as associated, visibly separate so it's never mistaken for a label baked into the chip itself. Tapping "+" gives it a distinct temporary active-state treatment (a filled tint plus a 3px border) — never the dark-green sent-fill "All" and "+" both stay outside that system entirely, since neither has anything to have been "sent." Tapping "+" again while active, or tapping anywhere outside the keyboard/docked-bar area, closes it without creating anything — no separate Cancel button; the old inline Add/Cancel buttons from the pre-docked-bar "+" flow are gone.
- Where content extends beyond the visible row, the last visible pill should be **partially cut off at the edge**, not a hard stop — a visible cue that more exists to scroll to, rather than the row appearing to simply end.
- **"Manage your Circles" removed from Going Quiet entirely (2026-08-11)** — confirmed via a full-app search that Going Quiet's picker was its only render site; nothing else in the app depended on that link for something Settings' own navigation doesn't already cover.

## Home naming and icon

Label stays **"Home"** even though the content underneath changes by state (Normal / Taking Time / Post-Reconnect) — nav labels name the destination the user returns to, not the momentary state, and "a stable place to come back to whatever state you're in" fits Hold's ethos rather than contradicting it.

The **icon** is what should change: not a literal house glyph, which is a generic pictogram unrelated to anything else in the app. Use Hold's own circle mark — the same shape as the main interaction circle — as the Home tab icon instead. This ties the nav bar back to the one shape that already carries the app's meaning (see `05-design-system/01-design-direction.md`) rather than introducing an unrelated symbol just for the tab bar.

## Settings panel structure

**Corrected:** not a single About screen with headed sub-sections — the hamburger opens a panel where each item is its own row, tapped through to its own screen. "Our Mission" (renamed from the generic "About") is one row among several, not the container for the others.

**Panel order, grouped by purpose rather than one flat list — revised from the original Mission-first order** (see `08-decisions/01-decision-log.md`): someone opening this menu while unwell is usually here to do something practical, not to read about the app's values, so task-oriented content leads and browsing/values content follows. Groups are separated by spacing alone, with no visible heading text — only the final group gets a divider line above it, since it's genuinely lower-priority legal/data reference rather than daily-use items.

**Build-status note, added 2026-08-12 after a live code check found the drawer's actual state materially behind an earlier optimistic write-up:** rows below are marked **Built** or **Not built — "Coming later" stub in code** to keep this spec honest against `hold-app`'s actual `SettingsDrawer.tsx`, rather than reading as a flat list of equally-real rows. See `07-business/06-business-strategy.md`'s "MVP status check" for the fuller verification detail this is drawn from.

**Manage Hold**

1. **Your Circles** — Built.
2. **Accessibility & Display** — **Not built.** New row, target design only — see "Accessibility & Display page" below. Supersedes the earlier separate "Accessibility" and "Personalise" rows implied by an earlier session write-up (referenced in `07-business/06-business-strategy.md`'s status check and the 2026-08-11 pricing decision-log row) — neither of those ever existed in code, and the merged single page below is now the intended target, not a further-split pair.
3. **Notifications** — **Not built** — an explicit `ComingLaterRow` stub in the current code, not silently missing.
4. **Language** — **Not built** — same stub treatment as Notifications.
5. **Connected Accounts** — **Not built** — same stub treatment as Notifications.

**About Hold**

6. **Our Mission** — Built. Values and privacy-values messaging in Hold's own voice, including the fuller version of "no one should be judged by their illness or its limitations."
7. **Research** — Built. The evidence base behind Hold's design and safety approach (accessibility research, safeguarding evidence, icon/label findings, and the lived-experience guilt-spiral/supportive-language research that shaped Hold's voice — see `02-research/`), surfaced honestly rather than left as internal documentation only. Can state plainly that Hold looked to the lived experience of people who deal with the guilt spiral when designing how it speaks: gentle, short, genuine statements that validate; permission without pressure or commentary. **Planned, not yet built:** the Research page needs individually addressable/anchored sections (not one undifferentiated block of text) to support the citation marker mechanism below — a requirement on this row specifically, not yet implemented.
8. **Hold+** — Built. See "Hold+ visibility" below for its other access point (Patterns' contextual surfacing).

**Support**

9. **Feedback** — Built.
10. **Share Hold** — Built. Invite someone else to Hold.

— divider line above this group only, since it's lower-priority legal/data reference rather than daily-use items —

**Legal and data**

11. **Privacy Policy** (link) — Built.
12. **Terms** (link) — **Not built** — same "Coming later" stub treatment as Notifications/Language/Connected Accounts above.
13. **Delete my data** — Built. Wipes every saved Circle, Hold history entry, in-progress reply, Conversations list, saved template, message draft, and remembered AI-drafting detail (including turning the AI memory toggle back off, not just clearing what it had captured) from the device, plus the anonymous AI-proxy install id (a fresh one is generated on next use, same as a genuine fresh install). Deliberately content-only: the one-time seen-welcome-screen/seen-retention-note flags are left alone, so a wipe doesn't force someone back through onboarding — see `08-decisions/04-open-questions.md`, "'Reset app' as a distinct action from 'Delete my data.'" Not part of the original panel spec, added here since it needed a home somewhere reachable

### Accessibility & Display page — target design, logged 2026-08-12, NOT YET BUILT

**Confirmed current status: none of this is built yet in `hold-app`** — this is the target design to build against, not a record of completed work. **Supersedes the earlier "separate Accessibility row and separate Personalise row" idea** referenced in an earlier session write-up — that split was never built, and is no longer the plan. Reasoning for merging into one page: font and display controls belong together, and a separate-rows split would create unnecessary navigation friction for settings someone is likely to want to adjust together.

One drawer row — **"Accessibility & Display"** — opens one merged page, organised into two sub-groups:

**Reading:**
- Text size
- Font — four options: System default, Lexend (visual-processing research basis), Atkinson Hyperlegible (Braille Institute, low vision), and OpenDyslexic (dyslexia-specific weighted letterforms). Verdana, Arial, and Open Sans were considered and explicitly cut as redundant with System default.
- Reduce motion (in-app override)

**Look & Feel:**
- Display theme (beach/forest/meadow/seasonal)
- Warmth bar — a relative offset applied on top of Hold's existing automatic warmth shifts per flow state, **not** an independent palette override. **Flagged, not yet confirmed:** WCAG contrast compliance must be verified across the full warmth range before shipping.
- Light/Dark/System toggle
- Moon phase toggle

**Spacing intent between groups:** Feedback/Share and Legal and data move together as one bottom-anchored block, pinned to the panel's bottom edge (mirroring the top padding above Your Circles) rather than trailing at a fixed distance below About Hold. The single largest gap in the panel sits above that whole block — the one real section break, between values/browsing content (Manage Hold, About Hold) and the practical, occasional-use rows below (Feedback/Share, then the divider, then Legal and data). None of the group spacing relies on a visible heading label, only breathing room (and, for the last group only, the divider line itself) to read as distinct sections.

**No icons in the drawer, deliberately, for now.** Considered and deferred rather than omitted by default — the same icon-plus-label accessibility reasoning used for the three bottom-nav tabs (`02-research/04-accessibility.md`: a familiar icon plus a short word lowers recognition effort versus text alone) would apply here too, but a dozen rows each needing a distinct, legible glyph is a meaningfully bigger design task than three tab icons, and plain text rows are already fully clear on their own. Worth revisiting once the drawer's contents settle, not a closed door.

**"Delete my data" uses a darker, muted red**, not the same red used for Circle-deletion/Hold-history confirms at their usual size and weight — the same destructive signal (this is the one truly irreversible action in the drawer) toned down for a passive row label sitting among plain-text rows, rather than an active confirm button, so it doesn't read as more alarming than the rest of the calm panel around it. See `05-design-system/02-colour-and-typography.md` for the derivation.

Bottom nav stays at three items — Home, Library, History. Settings deliberately does not become a fourth bottom tab, even though some reference apps (e.g. Balance) use an Account tab. Circles were already moved out of the bottom nav specifically because they're occasional maintenance rather than a reason someone opens the app; Settings sits in that same category, so it stays behind the corner icon rather than gaining equal billing with Home, Library and History.

## Hold+ visibility

**Revised: no persistent top-bar element.** A standing visual element in the top bar — even styled quietly — reads as ongoing pressure/visual noise, inconsistent with Hold's "held, not managed" tone. Supersedes the earlier two-access-point wording (see `08-decisions/01-decision-log.md`).

Two access points instead, both reaching the same destination:

- The Settings drawer's Hold+ row (above).
- Contextual surfacing at natural moments — currently the Patterns screen's "More with Hold+" section, shown below the free stats as an additive invitation ("here's more depth if it'd help you"), never a locked or greyed-out preview — see `03-product/04-patterns.md`.

Both now route to a concrete destination, `app/settings/hold-plus.tsx`: an honest info screen built from `07-business/02-pricing-principles.md`'s real content (free tier, what Hold+ would add, pricing — £17.99/year or £4.99/3-month, fair-access commitments), closing with a plain "not open for purchase yet" note rather than a working purchase flow, since no entitlement/billing system exists yet.

- Never a banner, modal, or interruption to the core journey (already established in `07-business/02-pricing-principles.md`).
- Never framed as urgency or a countdown — an invitation, not a wall.

## Circle setup

Circles are set up inline, during first use, as part of the natural Going Quiet flow — not as separate onboarding, so it doesn't feel like labour. "+ New Circle" and "Manage your Circles" are available directly from the Going Quiet screen. Ongoing management (editing, deleting, reorganising) lives in Settings.

## Personalise pattern — shared across Library and Reconnect (2026-08-11, corrected later the same day — Going Quiet no longer included; unified into one implementation 2026-08-20)

One rich per-person mechanic — a "Personalise" link/status that expands into an accordion with "What they sent," a "Starting point" chip row, "Your reply" (via the screen's own shared docked bar), and Save-for-later/Send-now actions. **As of 2026-08-20, Library's own standalone Conversations tab and Reconnect's embedded completion step are the same component and the same query logic, not two implementations independently reading the same store** — a `useConversations` hook (state/query/actions) paired with a `ConversationsView` component (rendering), replacing the earlier `usePersonaliseCompletion`/`PersonaliseCandidateList` pair (now deleted). This closed a real gap: the two entry points could show a different "what's pending" picture depending on which one was used, a trust problem for someone relying on Hold to keep things organised at low capacity, not just an architectural inconsistency.

- **Library/Conversations** — the mechanic's original home, **rebuilt 2026-08-12 for Circle-grouped people specifically:** each Circle chip in the top row now has its own independent dropdown arrow (matching Going Quiet's own circle/arrow pattern exactly); expanding it adds that Circle's people into one shared pill row directly beneath the chip row (not a separate quick-message-vs-Personalise swap per person any more) — tapping a person's pill always opens this same accordion, no simpler alternative. Sent-state (dark-green fill) shows per person here, not per Circle, reflecting that Conversations is a reply checklist across individuals, not a broadcast send. **Ungrouped people are unchanged**, still their own per-person link that swaps between a plain quick-message box and this accordion — a real, deliberate split between the two groups now, not an inconsistency. **A capability still not carried over for Circle members specifically, unchanged by the 2026-08-20 unification:** the manual "Conversation complete" mark (for a reply handled outside the app) has no home in the shared pill row and isn't currently reachable there; still present for ungrouped people's own cards.
- **Reconnect's completion step** ("everyone's been reached") — corrects the earlier plain "Personalise" button, which navigated straight to Library with nothing more specific happening on this screen. **As of 2026-08-20, this is no longer a flat list of accordions only — it's the full Library-equivalent experience** (per-person card, checkbox, Quick-message/Personalise swap), scoped to just this period's own audience rather than Library's unscoped everyone-ever-added list. Gains the permission-to-stop line and "Conversation complete" inside Reconnect's own flow for the first time, as a direct, intended consequence of sharing the same component — not a side effect to undo. Reconnect's own `send()` already seeds every audience member into Conversations at send time, so there's nothing extra to seed here, only to read back and render.
- **Going Quiet, corrected: does NOT use this pattern.** Briefly integrated the same day this section was first written, then explicitly removed later the same day — Personalise makes sense where there's an incoming message to reply to (Reconnect, Library); Going Quiet has no equivalent history to personalise against, and the heavier mechanic added cognitive weight at exactly the moment someone has the least capacity for it. Going Quiet's own replacement — spinning removed people into an ad-hoc new Circle — is documented in `01-core-journeys.md`'s Going Quiet section, point 5.

**What stays a plain navigation, deliberately:** Library's own reply flows (that's where the mechanic already lives) and the final "Finish Reconnecting" state (`app/return/done.tsx`). **Corrected 2026-08-11:** Reconnect's own completion step now always routes there once its OOO/Personalise decisions are resolved (previously it went straight home, a real asymmetry with Going Quiet's own `finish()` → `create/done.tsx` pattern that always lands on a calm completion screen) — `return/done.tsx` stays reachable from Library too, unchanged, for the case where someone gets there by finishing every Conversation instead.

## Library screen structure

**Revised:** the bottom-nav tab is called Library, not Conversations — but the screen itself leads with the Conversations reply-help experience, not the template shelf, so renaming the tab doesn't cost discoverability:

1. **Conversations** (primary, top of screen) — the per-person reply-help experience: paste in a message someone sent, get help wording a reply, tick/untick people as complete. This is what most people are actually there for, and it's what they see first.
2. **Templates** (secondary section, below) — saved messages (Messages / Emails / OOO / Social), built up over time via the "Save as template?" prompt, not present during onboarding.

Templates build up naturally over time: whenever the user edits an AI draft or writes their own message, Hold asks "Save as template?" — an explicit, opt-in prompt, not automatic capture. Over months this makes the section genuinely personalised without ever silently harvesting what someone writes.

**Template/chip explanations live here, not in the live composition flow.** The Going Quiet chip suggestions (e.g. "unwell," "overwhelmed," "need time") are deliberately compact and unexplained in the moment, to keep composition fast for someone who already knows what they mean. The fuller explanation of what choosing a given template actually communicates (matching the description text the original option cards used to carry, e.g. "Say your capacity is lower than usual") lives in Library instead — somewhere to look something up occasionally, not something repeated every time someone goes quiet. This resolves the trade-off of moving from descriptive cards to compact chips: the context isn't lost, it just moves to where it's actually useful rather than adding friction to the fast path.

A user opens Library because they need help communicating; Conversations is what they find immediately, Templates is what supports that once they're there.

## The Transition screen

**Resolved — the screen exists structurally now**, built as part of this session's flow work: Going Quiet → Transition → Taking Time is a genuine extra screen, not folded into Going Quiet's completion state. The "not yet decided" framing this section previously carried is superseded; see `04-ux-content/01-core-journeys.md` for the currently-shipped copy ("You've taken the first step. You've let the people who matter know you need some time. Taking time to recover isn't selfish. You don't need to earn rest.") and the Reconnect landing transition copy ("Welcome back. Here's who's waiting to hear from you. Reply however feels right today.").

### Planned copy + citation marker mechanism, logged 2026-08-11 — NOT YET DELIVERED TO THE APP

Drafted replacement copy for both transition moments, with a citation-marker mechanism, was written this session but never wired in — the app still runs the copy quoted above. **Flagged, not silently assumed as an upgrade:** this drafted copy would replace currently-shipped, working copy if built — treat this as a proposal to evaluate, not an obviously-approved update.

**Going Quiet → Transition screen, three lines in order:**
1. "This can feel harder than it should." — no citation marker.
2. "Taking time isn't the same as letting people down." — **citation marker**, linking to Holt-Lunstad et al. and/or Masi et al. research on the Research page (see `02-research/07-extended-evidence-base.md`, "Social connection / mortality" and "Loneliness interventions").
3. "You don't need to earn rest." — no citation marker. (Unchanged from the currently-shipped copy above.)

**Reconnect landing moment, same three-line shape:**
1. "Coming back doesn't need a perfect opening line." — no marker.
2. "Most people underestimate how much a message like this means." — **citation marker**, linking to Liu, Rim & Min and/or Boothby et al. research (see `02-research/07-extended-evidence-base.md`, "Reach-out underestimation / liking gap / compliance underestimation").
3. "It doesn't need to be perfect. It just needs to be sent." — no marker.

**Citation marker mechanism:** only the "common humanity" line in each sequence (the second line, in both cases) gets a marker — a small, muted, secondary-weight tap target (e.g. "Why this is true" in smaller/lighter text, not an academic footnote number), linking directly to the relevant anchored entry on the Research page. This depends on the Research page having individually addressable/anchored sections, not one undifferentiated block of text — see item 6 ("Research") in "Settings panel structure" above, where this requirement is also flagged as not yet built.

**Voice rules apply unchanged** to this drafted copy: no narrating the person's psychology back to them, no praising basic communication, no em dashes, no "should" as pressure, no exclamation marks — per `04-ux-content/02-voice-and-language.md`.

## No badges, no counts

Library never shows an unread count or notification badge on its nav icon. Reassurance in the Conversations section must stay opt-in — the person chooses to look, rather than the app creating ambient pressure every time they open Hold.
