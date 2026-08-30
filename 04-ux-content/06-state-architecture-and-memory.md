# State architecture and relationship memory

**Status:** Spec, not built. From an extended external design/research session (2026-08-19 onward), handed to this repo 2026-08-31. See `08-decisions/01-decision-log.md`, 2026-08-31. Read alongside `06-privacy-security/07-reconnection-safety-requirements.md` and `04-ux-content/07-universal-web-page.md` — this document's "no dashboard" rule is the same principle applied to a third surface.

## The four-layer Hold State Contract — every status carries these, kept separate

1. **Status** — what is happening ("I'm on Hold").
2. **Meaning** — what, if anything, the recipient should infer (user-selected: "nothing is wrong between us" / "this is about my capacity, not our relationship" / "I'm not able to talk about what this means" / "please don't make assumptions" / no meaning statement at all).
3. **Permissions** — what contact is welcome (messages welcome no reply expected / reactions only / urgent practical only / contact through a named person / please don't contact me / privately excluded).
4. **Private cause** — why, and how widely shared (entirely private / used only to generate wording / disclosed generally / disclosed to selected recipients / disclosed in detail to trusted people only).

**These four layers must never be fused into a single combined state.** A person can disclose a cause without accepting messages, or welcome messages without ever explaining the cause. Do not build a UI that forces these to move together.

**Critical, explicit override:** "nothing is wrong between us" must always be optional and never defaulted to true. A person leaving an unsafe relationship must never be pushed, prompted, or defaulted into providing that reassurance — see `06-privacy-security/07-reconnection-safety-requirements.md`.

**Accessibility — progressive disclosure required.** Presenting Status, Meaning, Permissions, and Private cause as one combined setup screen would violate the standing low-capacity design principle against too many simultaneous choices (`02-research/02-low-capacity-design.md`). Each layer should be its own step with a sensible default and an obvious way to skip ahead, not a single dense form. Every connection view, backlog entry, and status label introduced by this spec needs a screen-reader label distinct from its visual presentation — particularly the per-person contextual memory below, since it may combine several pieces of state (last message sent, boundary chosen, date) that need to read coherently aloud, not just visually. All text supports dynamic text sizing per the existing type-scale rule; no fixed-height rows that would clip a person's name or status text at larger accessibility sizes. Any tappable row (opening a connection, the single aggregate line in "What limited aggregate view is acceptable" below) meets the standard minimum touch target size (44×44pt iOS / 48×48dp Android).

## Only three main states, externally

- **On Hold** — reply expectations paused.
- **Connection held** — someone is keeping space without requiring a response.
- **Reconnecting** — the user has chosen to open a particular connection at a level that feels possible.

Everything else (schedules, privacy controls, blocks, message memory, technical state) stays behind the scenes until specifically needed — not surfaced as additional top-level states.

## The memory model — memory, not a dashboard

This is the load-bearing distinction of this entire document. Hold needs to remember relationship state. It must NOT present that memory as an operational list to process. The difference is where and how information surfaces:

**Correct pattern (build this):** information appears only in context, when the user opens that specific person's connection. Example: opening Maya's connection shows "You sent Maya a reconnect message on Tuesday. You chose short messages and 'start from today.'" This is not visible anywhere else, and nothing summarises it into a combined view.

**Incorrect pattern (do not build this):** a "Connections held" screen listing every relationship with status columns (Open / Reconnecting / On Hold / Practical only / No contact / Blocked privately), acknowledgement counts, or any operational-list presentation. This directly contradicts the standing no-dashboard, no-tally principle (no percentages, no completion rings, no "12 people left," no overdue labels) already established for the rest of the app (`04-navigation-architecture.md`, "No badges, no counts"). This is a correction carried in from the source material, not an open design question — the dashboard version must not be built.

**What limited aggregate view is acceptable:** at most, a single quiet, non-operational line such as "12 connections are being held" — a passive fact, not a list, not sortable, not filterable by status, and never showing per-person breakdown at that level. Tapping through should reveal only people relevant to the user's current action (e.g. people available to reconnect with right now), never a full status table.

## Blocking — completely separate from ordinary Hold views, always

Blocked people must never appear in ordinary Hold views, connection lists, or the "connections held" line count. Blocking lives in its own discreet safety/privacy area, entirely separate from "Held" and "Reconnecting" as if it were just another relationship status.

**Why this separation matters, not just as a UI preference:** seeing a blocked person's name in an ordinary list may itself be distressing; surfacing it there risks implying the block is publicly visible when it must never be (per `06-privacy-security/07-reconnection-safety-requirements.md`); it makes a safety action feel like unfinished relational work sitting in a queue; and it risks encouraging the user to "reconsider" a safety decision simply because it's visually adjacent to reconnection prompts. Hold remembers a block solely to enforce it, not to display it.

## Rhythms and schedules live in their own space, not alongside relationships

A person's reply day, quiet hours, or planned retreat belongs under a dedicated "My rhythms" area — not displayed alongside individual relationship connections. The main screen may quietly state something like "Your next optional communication window is Sunday," but only if the user has explicitly opted to see it, and never as a countdown.

## Backlog handling — per-person, never as a numeric roll-up

When reviewing what happened during an absence, present information **by person**, not as an aggregate count. Correct pattern: "Maya sent 12 messages. Three were marked no response needed. One practical question may still be current." This is still information delivered per-relationship, one at a time, at the point the user chooses to open it — not a running total displayed anywhere passively.

**Explicitly incorrect:** a summary presented as "24 messages received / 18 require no response / 3 invitations have passed / 2 practical items may still be current / 1 marked time-sensitive" is a numeric tally in every meaningful sense, even though it's categorised rather than a single number. Any backlog summary feature must be restructured into the per-person, one-at-a-time pattern above before being built — the aggregate-count version must not be implemented even as a first draft.

## "Start from now" and return without arrears

> Messages sent during a Hold do not automatically become obligations payable when the Hold ends.

Backlog choices, available per-Hold or per-relationship: start from now (earlier messages moved out of the active view, not deleted); keep marked-important items only; receive a private, per-person summary (never aggregate); archive silently (no alerts to senders, no read receipts generated, no rejection implied); or ask the sender to resend anything still relevant.

**"Ending Hold" must never, by default, trigger:** displaying every accumulated message at once, sending read receipts, notifying every contact that the user is available, delivering every drafted response, activating all muted conversations, exposing the return publicly, or changing every relationship to "open" simultaneously. Return happens in layers, one relationship at a time, each requiring the user's own action to advance.

## Research panel candidate — Settings → Research

> "Hold remembers your relationships so you don't have to keep track yourself — but it never turns that memory into a list to process. Information only appears when you open that specific connection, never as a summary of everyone waiting."

## Status

Not built in `hold-app` yet. Reference/spec material for future scoped feature work.
