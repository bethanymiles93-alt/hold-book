# History and Patterns

## Naming: Patterns, not Insights

**Decided.** "Insights" is common SaaS/dashboard language and doesn't fit Hold's tone. "Patterns" is a word people already use about their own health ("I've noticed a pattern," "there's a monthly pattern") — it reads as something the user is recognising about themselves, not something the app is analysing or judging them with. Keeps to the "observe, never diagnose" principle by the word choice alone, before any copy is even written.

## Where it lives

Not a separate bottom-nav tab. Patterns sits inside **History**, reached via a segmented control at the top of the screen: **History | Patterns**. History is where someone naturally goes to review previous quiet periods; Patterns is something checked occasionally, not a reason to open the app on its own — same logic already applied to keeping Circles and About off the bottom nav.

## History

A timeline of previous quiet periods, available to everyone (free and Hold+). Each quiet period is a card:

```
12–16 July
4 days Taking Time
Core & Work notified
Reconnected
```

Tap a card for more detail if the user wants it — the card itself is the calm, glanceable version; nothing is forced open.

## Patterns

Sits on the same underlying History data, but surfaces gentle observations rather than just a factual timeline.

### Free — Basic Patterns

- Number of quiet periods
- Average duration
- Time since last quiet period
- A single month's calendar view (current or a selected month), a basic grid with quiet days visually marked — no comparison across months, no trend detection, just what one month looked like
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

## Export

A natural extension of Patterns rather than a separate feature: a PDF or plain summary of quiet periods, durations and (if Patterns is active) the pattern observations — intended for the user to optionally take to a GP or therapist. The user controls what's included and when it's generated; nothing is sent anywhere automatically.

## Optional future layer: external comparison

Worth preserving as a genuinely future idea, not MVP or near-term Hold+ scope: comparing History against Apple Health/Health Connect or calendar data (e.g. "many of your quiet periods occur during the same phase of your cycle"). Same "observe, never diagnose" principle would apply, with explicit opt-in per data source. Not scoped or committed — flagged here so it isn't lost, not because it's planned.
