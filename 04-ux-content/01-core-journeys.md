# Core journeys

## Naming note

Earlier drafts of this book used "Create a Hold" and "Return from Hold" as the primary actions. Those have been superseded by the journey below. "Create a Hold" → **Going Quiet**. "Return from Hold" → **Reconnect**.

## The journey

```
Home
  ↓
Going Quiet
  ↓
Transition   (quiet acknowledgment, not celebration)
  ↓
Taking Time  (optional, repeatable — "Send an update" available)
  ↓
Reconnect
  ↓
Conversations   (per person: Quick message or Personalise)
  ↓
Reconnected   (quiet acknowledgment, once Conversations is complete)
  ↓
Home
```

**Decided:** both transition moments are real screens, not folded into existing states. This supersedes the earlier "not yet decided" status in `08-decisions/04-open-questions.md`.

- **Transition** (Going Quiet → Taking Time): a brief screen acknowledging the effort of what just happened, not congratulating in an overly cheerful way — someone may feel terrible. Example: "You've taken the first step. You've let the people who matter know you need some time. Taking time to recover isn't selfish. You don't need to earn rest." Primary button: "Begin Taking Time."
- **Reconnected** (Conversations complete → Home): mirrors the existing completion tone already used elsewhere ("The people who matter know. You can rest.") — a quiet acknowledgment, not a celebration screen. No confetti, no "Quiet Mode Ended" banner, just a brief moment before returning Home. Final copy: Heading "You're reconnected." Body "You've let the people who matter know you're here again. That's enough for today." Button "Done." Nothing more is required from the user here — it clears the Post-Reconnect state and returns to Normal.

Both screens are single-button, low-friction — they add a moment of acknowledgment, not extra decisions or extra taps beyond the one to continue.

Four emotionally distinct stages, kept separate on purpose:

1. **Going Quiet** — "I need space."
2. **Taking Time** — "I'm still here, but not ready." Optional and repeatable.
3. **Reconnect** — "I'm beginning to come back."
4. **Conversations** — "I'm ready to properly engage," at whatever pace that happens.

## Home

### Emotional goal
"I am safe here. I do not need to catch up."

### Three home states

| State | Main action | Secondary action |
|---|---|---|
| Normal | Going Quiet | — |
| Taking Time | Reconnect | Send an update |
| Post-Reconnect | Finish Reconnecting | Start a New Quiet Session |

**Post-Reconnect** appears when the user has entered Conversations but hasn't yet addressed everyone on the list (whether by Quick message or Personalise). It does not reset to Normal. Supporting copy: "Continue where you left off," optionally with progress ("2 of 5 replies sent"). Never use "outstanding," "incomplete," "overdue," "pending," or "you still need to."

The **Conversations** destination is separate from Post-Reconnect and always available, independent of whether the user has gone quiet at all — it's for getting help with a specific reply at any time, not only after a Hold journey.

### Avoid
- activity feeds
- overdue tasks
- streaks
- social comparison
- busy dashboards
- unread counts or badges on Conversations

## Going Quiet

1. Who needs to know? — choose one or more Circles. Circle setup happens inline here, not as separate onboarding, so it doesn't feel like labour ("+ New Circle" available on this screen; full management lives in Settings). Within a selected Circle, the user can untick individual people (send to most of the Circle but not everyone) and split out one or two people for a personalised message while the rest get the default — the granularity is per-person, not locked to the whole Circle at once.
2. What do you need them to understand? — select an intent or write your own.
3. Review recipients and message together.
4. Send (default: text/SMS to everyone, no extra channel decisions required; optional "Choose different channels" for people with a preferred contact method, configured later, never mandatory here).
5. Completion: nothing else to do. The person moves directly into Taking Time.

Suggested intents:
- I'm unwell
- I need some quiet
- Feeling a little overwhelmed
- Write my own

The Going Quiet message is the initial message and should never be described as an "update."

Example: "I'm not feeling well and need to take some time. I'll be in touch when I can."

## Taking Time

The resting state. No pressure, no default reminder to reconnect.

**Send an update** (optional, secondary, repeatable): lets the user reassure their Circles during a long quiet period without ending Taking Time or moving toward Reconnect.

Example: "I'm still taking some time and can't properly message yet, but I'm thinking of you."

**Add to Going Quiet** (edge case, low-key, not a prominent button): if someone new messages while the user is away, a small entry point lets them send a short "not feeling very well, will get back to you when I can" and adds that person to Hold's tracked list — this shouldn't be the norm, but happens and causes stress if unhandled.

**Going Quiet again, mid-Conversations** (distinct edge case): a user may need to go quiet again before finishing the previous round of Conversations. A small "Going Quiet" action stays available on the Conversations screen itself for this. When tapped, it does not return to Home first and does not ask the user to tap Going Quiet twice — it goes straight into a brief, auto-advancing transition (with a "Skip" option) and then directly into "Who needs to know?" Example transition copy: "We're glad you're here. Keeping your circles in the loop can ease worry, reduce misunderstanding and make reconnecting easier when you're ready." This keeps momentum for someone at very low capacity who might otherwise abandon the flow. Old unfinished Conversations remain saved rather than being cleared or lost — they stay available to pick back up whenever the new quiet period ends.

**Resolved — visibility timing:** "Send an update" is hidden on the calendar day the Going Quiet message was sent, and becomes visible from the next calendar day onward — simpler and more predictable than a session-based (close-and-reopen) trigger, which would behave oddly for someone who keeps the app backgrounded for days.

**Resolved — nudge default:** on by default, not opt-in, with an adjustable interval — an opt-in-only nudge mostly gets used by people who already knew to look for it, which undercuts the point for the people it would help most. What actually protects against frustration isn't the default, it's the delivery: this is a soft **in-app** prompt shown when the person happens to open Hold, never an OS push notification pinging their phone unprompted. Copy should explicitly mention "one tap to reassure, nothing else required" so the low effort is stated, not assumed. Honest caveat: no real interval has been researched yet — treat any specific number of days as a testable hypothesis, not evidence-based, until real usage data exists.

A future, optional gentle nudge may appear after a long quiet period: "You've been taking time for a while. Would you like to send a quick update? One tap, nothing else required." with "Send update" / "Not now" — never a countdown, never guilt-based wording. Framed as an invitation, not a reminder — "Would you like to reassure your circles?" rather than "It's been 5 days." The interval is user-adjustable in Notifications settings, not fixed.

## Reconnect

**Revised — single tap, symmetric with Going Quiet.** Tapping Reconnect is not followed by an upfront "how would you like to reconnect?" choice screen. It triggers a brief transition (acknowledgment, not a question — see below) and goes straight into Conversations. This keeps Home's two primary actions symmetric (both single taps), and moves the actual decision-making to where it's already needed: per person, inside Conversations.

**Transition copy:** "Welcome back. Here's who's waiting to hear from you — reply however feels right today."

### Audience

Reconnect persists the audience chosen at Going Quiet by default — there is no full re-pick screen. The user can still:
- remove someone already dealt with (e.g. spoken to on the phone)
- add someone new (e.g. someone who messaged while the user was away)
- expand to the full Circle — a bulk option to include everyone in the original Circle, not just the subset who received the Going Quiet message, for when the user wants to reconnect more broadly than the persisted list

Hold keeps account of who still needs a reply; this list is what Conversations reflects.

## Conversations

Available both as where Reconnect leads (per the restructure above) and as a standalone destination at any time, without needing to have gone quiet first.

**Structured in three tiers, matching how Going Quiet already groups people by Circle — not one flat list:**

### Tier 1 — Send to everyone
Top of the screen. One tap sends the same quick message (e.g. "I'm getting there, will respond properly soon") to the whole Reconnect list at once, for someone who doesn't want or need to address anyone individually or by Circle. This restores the original point of a single-tap Quick Connect within the per-person structure — without it, someone wanting the same message for everyone would have to repeat an action per Circle or per contact, which defeats "smallest possible decision."

### Tier 2 — Per-Circle
The list below "Send to everyone" is grouped under the Circles originally messaged at Going Quiet (e.g. "Family," "Work," "Book Club" as section headers), not a flat list of individuals. Each Circle group has its own bulk action — send one instant template to just that Circle — so different Circles can get different messages (e.g. a warmer note to Family, a brisker one to Work) without needing to act on each person separately.

### Tier 3 — Per person
Expand any Circle group to see and act on individuals within it. Per person, two lightweight options:
- **Quick message** — one instant, low-effort message, editable inline without leaving the page. Example: "I'm doing a little better, but I don't quite have the energy for a proper reply yet. I'll message properly soon x"
- **Personalise** — paste in the specific message they sent, get help wording a considered reply
- tick/untick as replied — always reversible, never a hard "done"
- "Conversation complete" covers: replied in Hold, replied elsewhere, phone call, saw them in person, or no further reply needed

### Adding someone new
A separate "+ Add person" action for anyone not part of the original Circles (e.g. a new contact who messaged while away) — added **one at a time**, not in bulk, since these are ad-hoc individual additions rather than an existing grouped Circle. They appear as their own item, not nested under an existing Circle group, unless the user chooses to also add them to a Circle.

**Accidental-tap protection applies at every tier**, not just Tier 1: any bulk action (Send to everyone, or a per-Circle send) shows a brief confirm step — "Send '[message]' to [N] people?" with Send / Cancel — before sending, given the page also has per-person tick boxes and buttons nearby. Using a bulk action at any tier doesn't block personalising a reply to any of those people afterward.

No counts, no unread badges, no "outstanding" language anywhere in this screen. "Hold remembers where you left off. Continue whenever you're ready."

## Technical wording rule

Native share sheets and non-SMS channels may not confirm delivery. Use "sent" only when the platform can truthfully confirm sending. For non-SMS channels, Hold prepares the message and hands off to the relevant share/app flow rather than claiming to send directly.
