# What personal content is kept, and for how long

Resolves the previously open "Keep this on your device for" retention window (see `08-decisions/04-open-questions.md`, now removed) and the deliberately-unplaced retention control noted on Personalise in `04-ux-content/01-core-journeys.md`.

Retention maps to whose content it is, and what it costs the user to lose — not one blanket rule.

## The three tiers

1. **Library** (saved templates) — permanent, no timer. Only ever holds the user's own words: a template they wrote or explicitly chose to save. Never contains anyone else's message. Low sensitivity by nature.

2. **Your own drafted text not yet sent or saved** — Personalise's "Your reply" box, and a Going Quiet or Reconnect message edited for one send without tapping Save. This is the effortful, personal, hard-to-recreate content, and gets the longest safety net: it persists through interruption and survives the app closing and reopening, clearing only on send, on deliberate discard, or after a 48-hour backstop. This must never punish someone who started a message, got interrupted, and came back — losing this content could stop a very ill person from reconnecting at all, which is the exact outcome Hold exists to prevent. An unsaved edit does **not** become a saved Library template unless the user explicitly taps Save; the two are always distinct copies.

3. **A pasted-in message from someone else** — Personalise's "What they sent" box. This is the most sensitive content on the device (another person's private message) but the cheapest to lose (it's re-pasteable), so both privacy and wellbeing point the same direction: clear it sooner. It clears on send, on the app fully closing, or after 4 hours, whichever comes first.

## Graceful behaviour, not an error state

If someone returns after the paste box has cleared but their reply is still preserved, the reply shows intact and the paste box is simply empty with its normal "paste their message here" prompt. No error, no "draft lost" alarm. It should read as tidying up after itself, not as something going wrong.

## Disclosure, not pressure

None of this is ever surfaced as a countdown, an expiry warning, or a deadline inside the flow — that would be exactly the guilt/pressure pattern Hold avoids everywhere else (see `04-ux-content/02-voice-and-language.md`'s governing voice principle). It's disclosed plainly in the privacy policy instead: drafts a person doesn't send are kept on their device for a limited time and then cleared automatically. At most, a one-time, calm mention appears the first time someone saves a Personalise reply for later, framed as reassurance ("Your reply stays on your device for a couple of days in case you need to step away. Their message clears sooner.") — never repeated, never a warning.

## Why "fully closing" rather than a pure timer for the pasted message

A mobile app's JS process doesn't keep running once it's genuinely killed, so the reliable, honest signal for "the app was fully closed" is the next cold launch, not a background timer that can't actually run. The pasted message clears on that signal in addition to its own 4-hour window — whichever happens first.
