# History and Patterns

## Naming: Patterns, not Insights

**Decided.** "Insights" is common SaaS/dashboard language and doesn't fit Hold's tone. "Patterns" is a word people already use about their own health ("I've noticed a pattern," "there's a monthly pattern") — it reads as something the user is recognising about themselves, not something the app is analysing or judging them with. Keeps to the "observe, never diagnose" principle by the word choice alone, before any copy is even written.

## Where it lives

Not a separate bottom-nav tab. Patterns sits inside **History**, reached via a segmented control at the top of the screen: **Your History | Your Patterns** (renamed 2026-09-01, matching the existing possessive convention already used for Your Circles and Your Wider World — found no rule scoping that convention to Settings specifically). History is where someone naturally goes to review previous quiet periods; Patterns is something checked occasionally, not a reason to open the app on its own — same logic already applied to keeping Circles and About off the bottom nav. Each segment's own eyebrow/title header text was removed the same day (2026-09-01) — both duplicated the tab label directly above; a dedicated History subtitle ("evidence of your effort and care," reframing the record as proof of effort rather than hard times) is planned separately, wording not yet confirmed.

## History

A timeline of previous quiet periods, available to everyone (free and Hold+). Each quiet period is a card:

```
12–16 July
4 days Taking Time
Core & Work notified
Reconnected
```

Tap a card for more detail if the user wants it — the card itself is the calm, glanceable version; nothing is forced open.

**Calendar and list merged into one page, decided 30 August (this section was stale until 2026-09-01 — described a separate List/Calendar toggle that was never the real decision).** No toggle between them: a calendar sits at the top, the card list always visible below it. **Always visible, not collapsible** (corrected same day, 2026-09-01, superseding an initial "collapsed by default, tap to expand" build — History's calendar is primary navigation here, not a secondary aid, so it stays open the same way the list below it always is). Header reads a plain "Calendar," no date repeated in it — the month/year are already visible in the calendar itself. Full calendar interactivity, matching standard calendar-app conventions:

- Only days with an actual logged period are tappable — an empty-day tap led nowhere before, pure friction for no benefit. Logged days carry a solid dark-green fill, reusing `AdaptiveCircleChip`'s own established sent-state colour pairing (not a separate calendar-only convention) — "this day has something" reads the same way "sent" does everywhere else in the app.
- Tap a date with activity jumps/anchors the list below to that entry, with a brief accent border marking which card it landed on. Widens the list's own default 6-month window first if the date's period is older than that, so there's always something to actually scroll to — confirmed 2026-09-01: History's own scrollback is genuinely unlimited/all-time for everyone, free and Hold+ alike (the underlying store has no cap or pagination), never gated.
- Tap the month name opens a month picker; tap the year opens a year picker, same row-of-pills mechanism used throughout the app.
- Picking a year reveals that year's twelve months as collapsed accordions underneath the calendar (not one long scrollable list) — tap a month to expand just its own entries inline, with one more control to expand or collapse every month in that year at once.

**Explicitly distinct from Patterns' own calendar, not merged into it:** History's calendar is the all-time record (every quiet period, any year) — a lookup tool, find a specific day and jump to what happened. Patterns' own monthly calendar (below) stays a separate, monthly-scoped view — a pattern-display in its own right, seeing the shape of a month's quiet periods at a glance, which is exactly why the same sent-state green marking matters there too. They're not redundant with each other. This is only about merging History's own internal list/calendar presentation into one page — the top-level Your History | Your Patterns segmented control above is unaffected.

## Patterns

Sits on the same underlying History data, but surfaces gentle observations rather than just a factual timeline.

### Free — Basic Patterns

- Number of quiet periods
- Average duration
- Time since last quiet period
- A single month's calendar view (current or a selected month), always visible — not collapsible, confirmed 2026-09-01, core to this screen's own value rather than a secondary aid. A basic grid with quiet days marked using the same solid dark-green sent-state fill as History's own calendar (not a separate lighter convention) — no comparison across months, no trend detection, just what one month looked like. Only logged days are tappable, same reasoning as History's own calendar. Free tier is locked to the current month only (prev/next/month/year navigation disabled); Hold+ unlocks genuine full-range browsing back to the earliest recorded period, same mechanism History's own calendar uses — confirmed 2026-09-01, though Hold+ itself isn't purchasable yet (dev/test flag only), so no real user can reach this range today regardless of tier
- Days spent Taking Time

### Hold+ — richer Patterns

- A multi-month calendar view (many months shown side by side or scrolled through together, not one at a time) plus actual trend detection across them, e.g. monthly or seasonal trends
- Recurring timing (e.g. "second week of each month")
- Changes over time (getting shorter/longer, more/less frequent)
- Optional health-note correlations, only if the user has recorded notes like PMDD or migraine themselves
- Longer-term summaries

**Decided:** Patterns exists for everyone at a basic level; Hold+ adds depth rather than withholding the feature entirely. This matches Hold's broader philosophy — the core experience is available to everyone, the paid tier makes it richer, not gated. This also resolves the earlier open question about whether to show Patterns as a locked upsell for free users: it isn't locked, it's a lighter version, so the paywall framing should read as "upgrade for more," not "unlock this."

### Example Hold+ observations

- "You've tended to go quiet around the same point each month."
- "Your quiet periods have been getting shorter over the last few months."
- "You've spent 24 days resting this year."
- "This is your fourth quiet period this year."

## What Patterns records

- When Going Quiet began
- When Reconnect began
- When the quiet period ended
- Total time spent Taking Time
- Number of quiet periods
- Average duration
- Recurring timing
- Optional user-added notes on a quiet period (free text, or quick tags like PMDD, migraine, flare, burnout, low mood, fatigue, custom)

## What Patterns deliberately does not record

This is a hard privacy boundary, not just a scope limit: Patterns does not measure number of messages written, length of conversations, message content, or how many replies someone sent. The only Conversations-related data point Patterns needs is that reconnecting started and that the quiet period was marked complete — nothing about what was actually said. Patterns is about the user's time away and health journey, not an analysis of their conversations.

## Design principle: observe, never diagnose

Already a stated Hold-wide principle (`01-foundation/03-principles.md`), and Patterns is where it matters most:

- Patterns describes what happened, in the user's own recorded data — it never names a condition, suggests a cause, or implies a clinical conclusion.
- No comparison to "normal" or population averages.
- No alerts framed as concerning ("You're going quiet more often" reads as a warning; "Your quiet periods have become more frequent this year" is a neutral observation the user can do what they want with).

## Export — two tiers, resolving a real ethical question

**Free, always, for everyone: raw data export.** A plain CSV/text list of quiet periods and durations, no formatting or analysis — the user's own data, available on demand at no charge. This matters beyond generosity: charging for someone's own raw data would sit uncomfortably against data portability norms (UK GDPR gives people a right to get their own data out, generally expected to be free) and would be a fair criticism of Hold if it charged for this. Never gate raw export behind payment.

**Paid, one-time, non-subscription: the Patterns Report.** A polished PDF — quiet periods, durations, and (if Patterns is active) the pattern observations, laid out and summarised. Useful for sharing with a doctor or therapist if that's what someone needs it for, but not framed as a medical document or restricted to that use — someone might just as easily want it as a general summary of their own year. This is priced because it's a service — the formatting and analysis work done on the user's behalf — not because the underlying data is being withheld. **£2.50 standalone, free with an active Hold+ subscription** (corrected 2026-08-20 from the earlier flat £2.99 — see `07-business/06-business-strategy.md` and `07-business/02-pricing-principles.md` for pricing; supersedes the earlier separately-priced £3.99 "GP/clinician PDF report" naming, see `08-decisions/01-decision-log.md`, 2026-08-11 correction and 2026-08-20 correction).

The user controls what's included and when either export is generated; nothing is sent anywhere automatically.

## Optional future layer: external comparison

Worth preserving as a genuinely future idea, not MVP or near-term Hold+ scope: comparing History against Apple Health/Health Connect or calendar data (e.g. "many of your quiet periods occur during the same phase of your cycle"). Same "observe, never diagnose" principle would apply, with explicit opt-in per data source. Not scoped or committed — flagged here so it isn't lost, not because it's planned.
