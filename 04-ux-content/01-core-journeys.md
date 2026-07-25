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

### Circle text hierarchy — previously undocumented

The main interaction circle carries a two-level text hierarchy in both its states, not a single line:

- **Normal (Going Quiet available):** "Going quiet" as the bold/larger in-circle header, "Tap to let your people know" as the smaller subtitle beneath it.
- **Taking Time (Reconnect available):** "Reconnect" as the bold/larger in-circle header, "Tap when you're ready" as the smaller subtitle beneath it.

This was a decision made early on but never actually written into this book, which is why it was missed in the first build — "Tap when you're ready to reconnect" as a single undifferentiated line is the bug this corrects.

### Avoid
- activity feeds
- overdue tasks
- streaks
- social comparison
- busy dashboards
- unread counts or badges on Conversations

## Going Quiet

1. Who needs to know? — choose one or more Circles. Circle setup happens inline here, not as separate onboarding, so it doesn't feel like labour ("+ New Circle" available on this screen; full management lives in Settings). Once a Circle pill is selected, a small down-arrow appears on it — tapping it expands a box beneath the picker row (collapsing any other Circle's expanded box first, only one open at a time, matching the Personalise pattern in Conversations) showing that Circle's recipients. Within it, the user can untick individual people (send to most of the Circle but not everyone) and split out one or two people for a personalised message while the rest get the default — the granularity is per-person, not locked to the whole Circle at once. This is the same interaction as Conversations' down-arrow expand pattern (breaking a Circle down to individuals), just reached from Going Quiet's picker instead — one consistent expand-a-Circle pattern across both screens, not two different mechanisms that happen to do similar things.
2. What do you need them to understand? — **first message to a given Circle only:** select an intent (chips: I'm unwell / I need some quiet / Feeling a little overwhelmed / Write my own) or write your own, edit if wanted, then tap **"Save to Library"** near the message box — with a short line beneath it, e.g. "This becomes your usual message for [Circle]. Edit it anytime in Library," so the mechanism is stated plainly rather than happening silently. This stores the message as that Circle's saved default. **Subsequent messages to the same Circle:** the chips don't reappear — the message box is pre-filled with the saved default, directly editable in place, with a small "Change template" link remaining available as a low-profile escape hatch (not full chips again) for the occasion someone wants to switch approach entirely. The same "Save" affordance stays available on every visit: editing the wording and tapping Save updates the stored default going forward; editing without tapping Save applies only to that one message, leaving the stored default unchanged — someone tweaking a message once shouldn't accidentally overwrite their usual default without meaning to. The default can also be changed any time in Library directly.
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

**Transition copy:** "Welcome back. Here's who's waiting to hear from you. Reply however feels right today."

### Audience

Reconnect persists the audience chosen at Going Quiet by default — there is no full re-pick screen. The user can still:
- remove someone already dealt with (e.g. spoken to on the phone)
- add someone new (e.g. someone who messaged while the user was away)
- expand to the full Circle — a bulk option to include everyone in the original Circle, not just the subset who received the Going Quiet message, for when the user wants to reconnect more broadly than the persisted list

Hold keeps account of who still needs a reply; this list is what Conversations reflects.

### Reconnect screen — three actions, Conversations hidden until triggered

The Reconnect screen (labelled "Reconnect," since tapping the Reconnect button brought the person here) opens with the message ready and exactly three actions:
- **Send** — sends the instant message to the current selection.
- **Edit** — basic in-place edits to the template text, without leaving the screen.
- **Personalise** — leads into Conversations (below) for a fuller, per-person reply.

**Conversations does not appear on this screen until something has actually happened** — either an instant message has been sent, or Personalise has been tapped. Before that, the screen is just Reconnect: message, Send, Edit, Personalise. This avoids showing two routes to the same place at once (Personalise and a visible Conversations section would be redundant), and protects the calm default view.

**Resolved — the gate is Send-only.** Tapping Personalise goes straight into Conversations with no intermediate prompt, since choosing Personalise already answers "do you want to reply to anyone properly" — asking again would be redundant. Because tapping Personalise *is* entering Conversations, the two are one door, not two. The gate prompt only appears after **Send**: **"Want to reply to anyone properly?"** with a "Not now" option alongside Personalise itself as the other path forward. "Not now" skips straight to the Reconnected screen and back to Home — completing Reconnect with just the instant message, and no further personalising, is fully valid, nothing is forced.

### Instant message status label

Immediately after sending: **"Sent. They know you're thinking of them."** — brief and warm, stating what was achieved for the relationship without praising the person or naming their psychology (per the governing voice principle in `04-ux-content/02-voice-and-language.md`). From the next calendar day onward, the label becomes the actual date instead (e.g. "Sent 26 Jul"), since "sent" alone goes ambiguous the longer Taking Time continues.

## Conversations

**Revised again — two separate dropdowns, not one progressively-revealing section.** The previous version nested per-person instant messages inside the same area as the bulk flow. This version splits by *purpose* instead: a **Quick message** dropdown for the low-effort bulk case, and a **Personalise / Conversations** dropdown for anyone who needs actual attention — someone moves from one to the other by being unticked, rather than gaining a third nested level within the same section.

**The screen is organised around "who, then how"** — selection answers *who*, the two dropdowns answer *how*.

Available both as where Reconnect leads and as a standalone destination at any time, without needing to have gone quiet first.

### Dropdown 1 — Quick message (top)

**Default view — two elements only:** a scrollable Circle selection row mirroring Going Quiet's picker ("All" first, then each individual Circle), and one shared message box beneath it with one Send action. That's the whole dropdown for someone happy to send the same quick message to everyone.

**When "All" breaks** (any Circle deselected): reveals one row per Circle, all of them, each with its own message box pre-filled from a copy of the shared box (or that Circle's own saved default if one exists), independently editable, its own Send action, and a down-arrow to expand into its people.

**Unticking someone from a Circle's group removes them from Quick message entirely — they move to Dropdown 2**, not into a nested individual instant-message box within this dropdown. Quick message's whole purpose is the low-effort bulk case; anyone who needs individual attention belongs in the other dropdown, not a third tier bolted onto this one.

**Sent-state pill treatment:** once a Circle's message is sent, its pill softens and desaturates to a paler, quieter version of its own colour, paired with a small checkmark — and **loses the outer selection halo/border**, since "sent" is its own distinct state, not the selection indicator layered underneath it. Never a full colour inversion (white fill/dark green text is already assigned to secondary navigation/add-manage actions elsewhere).

**Status label evolves over time, not a single frozen state:** immediately after sending, the label reads "Instant message sent." From the next calendar day onward, it changes to show the actual date instead (e.g. "Sent 26 Jul") — "sent" alone becomes ambiguous the longer Taking Time continues, but is perfectly clear in the moment it happens.

### Dropdown 2 — Personalise / Conversations

Contains: anyone unticked out of a Quick message group, anyone added via "+ Add person," and is also the standalone destination reachable independent of having gone quiet at all — someone can open it because they have one hard message to reply to, with nothing else required first.

Per person:
- **Personalise** — expands as an accordion panel directly beneath that person's row, not a separate screen. Only one panel open at a time. Panel contents: "What they sent" paste box; "Starting point" as a compact horizontal row of chips (Keep it brief / Acknowledge the wait / Explain a little / Write my own); "Your reply" text box, pre-filled from the chosen starting point, editable; send-now/save-for-later actions. Closing the panel collapses it back to a compact status row. The retention-duration control from the original full-screen version is deliberately left unplaced here pending clarification — see `08-decisions/04-open-questions.md`.
- tick/untick as replied — always reversible, never a hard "done"
- "Conversation complete" covers: replied in Hold, replied elsewhere, phone call, saw them in person, or no further reply needed

**Post-send state.** After a Personalise reply is sent, the row's status label reads "Sent. They'll hear from you properly." (same next-day-becomes-a-date behaviour as the instant message, and same voice principle — warm, brief, no praise). Sending does not automatically tick the conversation as complete — that stays a separate, deliberate action, since "Conversation complete" already covers real-world completion paths beyond "Hold sent something."

### Adding someone new

"+ Add person," in Dropdown 2, for anyone not part of the original Circles (e.g. a new contact who messaged while away) — added one at a time, not in bulk.

### Accidental-tap protection

Applies to any bulk action in Dropdown 1 (the shared "All" send, or a per-Circle send): a brief confirm step — "Send '[message]' to [N] people?" with Send / Cancel — before sending.

No counts, no unread badges, no "outstanding" language anywhere in this screen. "Hold remembers where you left off. Continue whenever you're ready."

## Technical wording rule

Native share sheets and non-SMS channels may not confirm delivery. Use "sent" only when the platform can truthfully confirm sending. For non-SMS channels, Hold prepares the message and hands off to the relevant share/app flow rather than claiming to send directly.
