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

### Four home states

| State | Main action | Secondary action |
|---|---|---|
| Normal | Going Quiet | — |
| Taking Time | Reconnect | Send an update |
| Reconnecting | Continue reconnecting | — |
| Post-Reconnect | Finish Reconnecting | Start a New Quiet Session |

**Reconnecting** (new, added with Reconnect's multi-select/completion-gate rewrite) appears when Reconnect's coverage gate hasn't been satisfied yet — whether the user just navigated away mid-session or force-quit and reopened the app. Resumes straight back into the picker, not a fresh start. Supporting copy mirrors Post-Reconnect's pattern: "Pick up where you left off," with progress ("2 of 5 reached") when available.

**Post-Reconnect** appears once the coverage gate is satisfied and the user has entered Conversations but hasn't yet addressed everyone on the list (whether by Quick message or Personalise). It does not reset to Normal. Supporting copy: "Continue where you left off," optionally with progress ("2 of 5 replies sent"). Never use "outstanding," "incomplete," "overdue," "pending," or "you still need to."

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

**One single scrollable screen, no separate Review step.** Send is the one urgent, essential action, done immediately — everything else (going deeper on a specific person, email out-of-office, wider-world status) is a calm, optional unwind that happens *after* Send, never gating in front of it. This mirrors the shape Reconnect already uses: essential action first, "want to do more?" second.

Top to bottom:

1. **Who needs to know?** — choose one or more Circles, from the same single row of Circle chips used throughout this screen (not a separate audience-picker row plus a separate send-picker row — one row does both). Circle setup happens inline here, not as separate onboarding ("+ New Circle" available on this screen; full management lives in Settings). A Circle created here this way stays local to this session — whether to make it a real, persisted Circle is asked later, at Reconnect, once capacity has likely improved, never here (see point 4 and Reconnect's own section below).
2. **Per selected Circle, a card**, always visible (not behind an expand/collapse) — one consistent place for this, not a mechanism duplicated between the picker and the message section:
   - Every recipient shown with a **selection circle** — the same visual language as Home's main action circle: solid filled when included in the Circle's shared message, white with a border when excluded. Colour is always paired with the fill change, never colour alone.
   - The shared group message box (see point 3) — goes to everyone still included.
   - Beneath it, anyone excluded from the group message gets their own row: a second-level selection circle, their own short instant message (pre-filled from the Circle's current shared draft, then independently editable), and a **Personalise** link. Tapping Personalise routes them to Conversations instead of sending an instant message — deferred: nothing is seeded into Conversations until Send actually fires, since there's nothing real to show there before that.
   - Tapping that same second-level circle again fully removes the person instead — their row collapses to just their name, muted, no box, no link, minimal weight. Tapping it once more restores them exactly as they were (box and Personalise link reappear, their message text was never lost). One consistent control throughout, never a swipe gesture and never a separate "Remove" link. **Exception: a Circle with only one contact never shows this second-level control at all** — fully removing that one person already has the same effect as not selecting the Circle in the first place, so offering a redundant second way to reach the same outcome would just be confusing.
3. **The shared message box** — **first message to a given Circle only:** select an intent (chips: I'm unwell / I need some quiet / Feeling a little overwhelmed / Write my own) or write your own. **Whatever generic text this produces auto-persists as that Circle's saved default immediately — no separate "Save" tap needed for the pristine, unedited pick.** **Subsequent messages to the same Circle:** the chips don't reappear — the box opens pre-filled with the saved default, directly editable, with a small "Change template" link as a low-profile escape hatch back to the chips. **Editing** that text only carries forward if the user explicitly taps **"Save to Library"** — with a short line beneath it, e.g. "This becomes your usual message for [Circle]. Edit it anytime in Library." An edit made without tapping Save applies to that one message only; the next visit shows the original saved default again, not the abandoned edit. **When more than one Circle is selected:** each Circle keeps its own card and its own box — never one shared box for the whole send.
4. **Send — per-Circle and repeatable, not a single whole-screen action fired once.** The same one Circle-chip row from point 1 doubles as the send picker — no second row. For a Circle not yet sent this session, tapping its chip behaves exactly as it always has (adds/removes it from the audience; its card, once added, stays visible unconditionally, not behind a select-to-expand step). Only once a Circle has actually been sent does its chip's tap meaning change: it switches to the sent/checkmark look (in place, same position in the row — never a new row or a line of its own), its card collapses, and tapping it now means "reselect" (reopens the card, ring/highlight appears) rather than "remove from audience" — removing an already-sent Circle wouldn't undo its message, so that action stops making sense once sending has actually happened. Send fires for whichever cards are currently visible (every not-yet-sent Circle, plus any sent Circle currently reselected): the group message to everyone still included in each, each excluded-and-not-personalise-tapped person's own instant message, and seeds anyone who tapped Personalise into Conversations' Personalise bucket. Taking Time actually begins at the first successful Send. The screen never auto-completes or locks after one Send — it's fine to send to some Circles now and others later, in any order, rather than requiring everyone at once. No screen-level "Sent" confirmation line — the per-Circle checkmark + colour change already satisfies "never rely on colour alone" at the individual level, and a blanket "you've communicated to everyone" line would no longer be accurate once sending is partial/repeatable rather than one-shot. The restful "you've done what's needed" feeling belongs on the Transition screen instead, not stacked here on top of an already-satisfied per-chip signal.
5. **"Want to send anyone something more personal?"** — Yes / Not now. Re-offers the excluded people belonging to Circles that have actually been sent so far (not the whole audience — a Circle that hasn't been sent yet has no one to personalise about), whether or not they were already routed to Personalise, with an inline compose box each — not a navigation, an alternative way to reach the same depth right here. Mirrors Conversations' own "an instant message doesn't preclude a fuller follow-up" allowance.
6. **Email out-of-office**, then **"Set your status elsewhere"** — appear here, once anything has been sent, not before it. Purely optional toggles.
7. **"Done"** — one explicit, deliberate final tap (not automatic — an untouched toggle is ambiguous about whether someone decided "not now" or just hadn't got to it yet, and this app's own low-capacity design principles argue against an unclear automatic trigger), reachable as soon as at least one Circle has been sent — it doesn't require every selected Circle to be sent first. Activates out-of-office and copies the status text if either was enabled, then moves on to the Transition screen ("You've taken the first step...", unchanged).

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

Structure: "All" plus one pill per Circle in a single horizontal scrollable row, reusing Conversations' own Quick-message chip styling — but multi-select here (each pill toggles independently; "All" is a select-all/none convenience, not an exclusive third option), not the single-select "All or one Circle" choice Quick message uses. No gating step; the message box sits directly below, available immediately. One shared message box for whichever Circles are currently selected — sending a genuinely different message to a different Circle means visiting this screen again separately, not multiple boxes open at once. Sending switches each just-updated Circle's pill to the same in-place sent/checkmark treatment used elsewhere, without reordering it. A Circle already marked sent can still be selected again for a further update — its sent look steps aside while selected, and returns if deselected without sending.

After Send: a brief calm line ("You've updated the people you need to. Well done.") then an automatic return to Taking Time — nothing to actively dismiss.

A Circle's "already sent" state persists across re-opening this screen within the same Taking Time period, but resets once a new Going Quiet round begins — it lives in the same flow state that already resets at that boundary elsewhere in the app, not a separate mechanism.

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

Reconnect persists the audience chosen at Going Quiet by default — there is no full re-pick screen. The user can still add someone new (e.g. someone who messaged while the user was away, via "Add to Going Quiet"); the full audience — every Circle and every ungrouped individual — is what the picker below reflects.

**Revised: no separate "remove someone already dealt with" escape hatch.** The completion gate below requires everyone in the audience to be reached by an instant message at least once before Reconnect's second stage unlocks — there's no way to mark someone as handled outside Hold (e.g. a phone call) and skip them. This supersedes the earlier allowance; flagged here since it's a real capability loss, not just a rewording, in case it needs revisiting.

### Reconnect screen — multi-select picker with a completion gate

Replaces the previous three-action (Send/Edit/Personalise) single-audience-box screen. Structure:

1. **Picker**: "All" plus one pill per Circle and one pill per ungrouped individual, in one horizontal scrollable row — the same multi-select + All pattern used throughout the app (Going Quiet's Circle picker, Taking Time's "Send an update"). Can select everyone, a subset, or narrow down to just one person.
2. **One shared message box** for whichever are currently selected.
3. **Send** — sends the message to the current selection; each just-reached Circle/individual's pill switches to the existing sent/checkmark treatment in place. Repeatable across as many separate sends as needed to reach everyone.
4. **Coverage gate**: until every Circle and every ungrouped individual has been reached at least once (a plain "X of Y reached" line makes progress visible), the picker/box/Send loop is the only thing on screen — no Personalise, no "want to reply properly," nothing else competing for attention before the essential thing is actually done.
5. **Once fully covered**: for each Circle created inline during Going Quiet and never made permanent, **"Add [name] to [Circle] permanently?"** — Yes / Not now, one at a time, ahead of everything below. This is where that question belongs, not Going Quiet — asking someone to make a structural decision about Circle permanence in the moment of going quiet contradicts the app's own low-capacity design principles; by Reconnect, capacity has likely improved. Then: "Want to reply to anyone properly?" → **Personalise** (leads into Conversations, unchanged) / **Not now** (returns to Home, unchanged — see below). Also newly unlocked here: **"Turn off out-of-office"** and **"Clear my status,"** shown only if either was turned on at Going Quiet's "Done" step. Both are currently mocked, symmetric to how activation itself is mocked — no real email/social provider integration exists yet.

**"Not now" still returns to Home, not straight to Reconnected**, unchanged from the prior resolution: the instant messages alone don't mark anyone in Conversations complete, so Home resolves to Post-Reconnect ("Finish Reconnecting" available) rather than a forced acknowledgment. Reconnected only ever fires from Conversations/Library's own completion check.

**Force-quit resilience, by design, not an afterthought.** Coverage (who's been reached) is stored on the Hold period record itself, not just in-memory app state — closing the app mid-Reconnect and reopening resumes exactly where it left off, with Home showing "Continue reconnecting" (with the same "X of Y reached" line) rather than a misleading Normal state. See `docs/03-privacy-model.md` for what's stored and why.

### Instant message status label

Each reached Circle/individual's pill switches to the same in-place sent/checkmark treatment already used in Library's Quick message and Taking Time's update screen (desaturated fill, checkmark, name) — no separate full-screen status label, since the picker itself is always showing current state rather than a single one-shot confirmation.

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

**Sent is reopenable, not a permanent lock:** tapping a sent Circle's pill (or, when "All" is fully sent, the shared "Sent to everyone" summary in its place) reopens the same message box and Send action for another round, rather than leaving no way to message that Circle or everyone again for the rest of the Conversations session. A repeat send updates the status label's timestamp to the new send.

### Dropdown 2 — Personalise / Conversations

Contains: anyone unticked out of a Quick message group, anyone added via "+ Add person," and is also the standalone destination reachable independent of having gone quiet at all — someone can open it because they have one hard message to reply to, with nothing else required first.

**Build note:** the standalone "reply without having gone quiet" entry point is intentionally not wired up yet — it's meant to live inside Library (`04-ux-content/04-navigation-architecture.md`, "Library screen structure"), which hasn't been built. This isn't a regression; there's deliberately no route to it until Library exists.

Per person:
- **Personalise** — expands as an accordion panel directly beneath that person's row, not a separate screen. Only one panel open at a time. Panel contents: "What they sent" paste box; "Starting point" as a compact horizontal row of chips (Keep it brief / Acknowledge the wait / Explain a little / Write my own); "Your reply" text box, pre-filled from the chosen starting point, editable; send-now/save-for-later actions. Closing the panel collapses it back to a compact status row. "What they sent" clears automatically after 4 hours or when the app is fully closed, whichever comes first; "Your reply" persists for up to 48 hours to protect an in-progress reply through interruption, clearing only on send or deliberate discard. Neither is ever shown as a countdown or warning in the flow. See `06-privacy-security/04-content-retention.md` for the full three-tier retention model.
- tick/untick as replied — always reversible, never a hard "done"
- "Conversation complete" covers: replied in Hold, replied elsewhere, phone call, saw them in person, or no further reply needed

**Post-send state.** After a Personalise reply is sent, the row's status label reads "Sent. They'll hear from you properly." (same next-day-becomes-a-date behaviour as the instant message, and same voice principle — warm, brief, no praise). Sending does not automatically tick the conversation as complete — that stays a separate, deliberate action, since "Conversation complete" already covers real-world completion paths beyond "Hold sent something."

### Adding someone new

"+ Add person," in Dropdown 2, for anyone not part of the original Circles (e.g. a new contact who messaged while away) — added one at a time, not in bulk.

### Accidental-tap protection

Applies to any bulk action in Dropdown 1 (the shared "All" send, or a per-Circle send): a brief confirm step — "Send '[message]' to [N] people?" with Send / Cancel — before sending.

No counts, no unread badges, no "outstanding" language anywhere in this screen. "Hold remembers where you left off. Continue whenever you're ready."

## Amend with AI (Hold+)

A Hold+-gated light-touch edit, not a from-scratch regenerate — the same mechanism appears in the same position on four surfaces: Going Quiet's per-Circle box, Reconnect's box, Taking Time's "Send an update" box, and Personalise/Conversations' reply box.

- **Position:** a link/button directly below the message box, above Send — same spot on every screen it appears.
- **Panel:** tapping it opens a small panel with an open prompt, "What's going on, if you want to share?" Generating blends whatever's currently in the box (a template, an edit, or blank on Personalise, which starts empty since there's no template there) with the typed context — the model is instructed to change only what the new context requires and keep the rest, never a full rewrite. Re-editing the prompt and tapping again regenerates. "Done" replaces the box content with the result and collapses the panel back to the single-box layout — only one Send button ever exists per screen.
- **Always present regardless of Hold+ status:** manual editing of the box itself. Amend with AI is additive; it's absent entirely for free users (not greyed out or locked), never the only way to change a message.
- **Personalise's pinned "What they sent" box:** once populated, settles into a muted, read-only-looking card (the same desaturated treatment as an existing sent-state pill, not the selection-circle green) with a visible "Edit" control — no hidden gesture. Stays visible throughout drafting and after Done; it never collapses.

### AI memory — a separate, further opt-in

Two layers, both required before anything is captured or shown:

- **Layer 1:** a standing toggle, "Remember helpful details for drafting and notifications," off by default, set ahead of time in the Hold+ area — never offered as an in-the-moment prompt during Going Quiet or Reconnect.
- **Layer 2:** only if Layer 1 is on, the same Amend-with-AI request may also ask the model to quietly note a short, relevant detail — no interruption at the moment of drafting. Later, during Taking Time or Reconnect specifically (never Going Quiet), the oldest unused note surfaces as a dismissible suggestion: "Use it" feeds it straight into that screen's own Amend-with-AI prompt (kept afterward, but not suggested again); "Don't remember" deletes it outright. If Layer 1 is off, Layer 2 never surfaces anything, and turning Layer 1 off deletes every note already stored.
- **Retention:** 90 days from creation, confirmed as a standalone figure rather than tied to any trial or subscription mechanism — long enough to cover a real illness cycle end-to-end, short enough to avoid indefinite retention of personal details. See `docs/03-privacy-model.md` (in `hold-app`), "AI memory."
- **Not included:** using this data for Patterns/analytics — drafting-only for now; that would need its own separate disclosure and decision.

The Hold+ info screen carries a fixed, illustrative before/after example of Amend with AI (clearly labelled as a static example, not a live preview) alongside its existing feature list.

## Technical wording rule

Native share sheets and non-SMS channels may not confirm delivery. Use "sent" only when the platform can truthfully confirm sending. For non-SMS channels, Hold prepares the message and hands off to the relevant share/app flow rather than claiming to send directly.
