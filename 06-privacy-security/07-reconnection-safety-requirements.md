# Reconnection safety requirements

**Status:** Active, hard requirement — not a design preference.
**Priority:** Same tier as Phase 10 (Hold+ monetisation) and the accessibility audit. Governs the entire recipient-facing surface of the app.
**Source:** Extended external design/research session, 2026-08-19 onward, handed to this repo 2026-08-31. See `08-decisions/01-decision-log.md`, 2026-08-31.

## The requirement

**Reconnection must never be compulsory.** Every recipient-facing Hold experience must preserve a private, non-signalling way to decline contact, remain silent, mute, restrict, or permanently block. The other party must not be told which protective action was taken, and no explanation may be required.

**Why this is a hard requirement, not a caveat:** restorative, repair-oriented language, applied without an escape hatch, is exactly the kind of framing that can pressure someone into re-engaging with a controlling or abusive relationship. This is a precondition of the Reconnect design, not something layered on top of it. Every other decision about Reconnect copy, flow, and notifications must be checked against this requirement, not the other way round.

## Mandatory sub-requirements — implement all of these, not a subset

1. **Declining must not send a rejection notification.** The other party receives nothing that signals a decline occurred.
2. **Blocking must not be exposed through a special Hold status.** No visible state exists that means "this person blocked me via Hold" as distinct from ordinary non-response.
3. **No read receipt may reveal that a return request was viewed.** Viewing and declining must be indistinguishable from never having seen it.
4. **No countdown, reminder, or streak may pressure a response**, on either side of the interaction.
5. **Repeated contact attempts must not bypass a boundary.** If a person has muted, restricted, or blocked someone, later attempts by that person to reach them through any Hold surface must not create new prompts, notifications, or exceptions.
6. **Mutual contacts or "bridge people" must not be recruited without explicit, specific consent** — applies directly to the bridge-person idea logged in `08-decisions/04-open-questions.md`; this requirement constrains that feature's eventual design, not the reverse.
7. **Safety actions must not require composing a message.** Declining, muting, restricting, or blocking must be completable via a single interaction, never gated behind "explain why" or "send a message to confirm."
8. **A person must be able to leave the relationship without completing a reconciliation flow.** No safety action should be positioned as a step inside, or a failure exit from, the repair/reconnection sequence — it must be a first-class, independently reachable action.
9. **The interface must never rank reconciliation as the "successful" outcome and separation as failure.** No visual treatment, copy, or flow structure should imply that ending a relationship or blocking someone is a worse or incomplete result compared to reconnecting.
10. **Explanations, health details, and evidence of incapacity are never owed** — to the other party, and not required by the app as a condition of taking a safety action.
11. **Safety controls must be accessible but discreet** — reachable without deep navigation, but not visually flagged in a way that would let someone looking over the user's shoulder easily infer they're being used.

**The load-bearing phrase across all eleven is "undiscoverable by the other party."** The system must reveal no more than ordinary non-response ever would. It must never surface anything equivalent to "Bethany declined reconnection," "Bethany blocked you," or any status label, icon, or copy that leaks a safety decision to the person it was taken against.

## Where this applies

Audit every recipient-facing surface against this requirement, including but not limited to:

- Reconnect flow (both directions — the returning person's experience and whatever the recipient sees)
- Conversations / address-list features
- Any future "bridge person" or trusted-intermediary feature (`08-decisions/04-open-questions.md`)
- Any future "recipient view" feature (`08-decisions/04-open-questions.md`)
- Notification copy and triggering logic anywhere a status change could be inferred
- Read-receipt or "seen" indicators anywhere in the app
- The universal web page (`04-ux-content/07-universal-web-page.md`) and its acknowledgement mechanism
- The glyph/state system (`05-design-system/03-glyph-and-state-system.md`)
- The relationship-memory model (`04-ux-content/06-state-architecture-and-memory.md`)

If a feature is proposed later that would violate any sub-requirement above, it should be flagged back rather than built, even if it wasn't explicitly anticipated by this list — the governing test is the requirement itself, not this list's completeness.

## Governing copy principle — applies to all Hold language, not just Reconnect

> Absence is not evidence of wrongdoing. Reconnection is an invitation, not an obligation. Repair is offered only when the user identifies something they wish to repair. Safety and separation remain valid at every stage.

Practical consequence for copywriting: the *default* Reconnect pathway must never presume wrongdoing, impact, or the need for repair — not even in a soft "acknowledge the impact" form, since that still risks converting another person's possible reaction into the absent person's presumed fault. A separate, explicitly opt-in pathway (entered only by the user's own affirmative choice, never inferred from message-count, duration, or the other person's visible distress) is where repair-oriented language belongs. See `02-research/08-cross-cultural-withdrawal-and-repair.md`'s "Formal Reconnect-phase architecture" section for the full default-vs-repair pathway structure and the verified apology-element checklist.

## Status

Not built in `hold-app` yet. This document is the governing constraint for all Reconnect-adjacent work going forward — confirm any new Reconnect/Conversations/bridge-person/recipient-view feature against it before implementation, and flag back rather than silently override if an existing shipped behaviour turns out to conflict with it once audited.
