# Product overview

## Core jobs

### When capacity drops
“Help me tell the right people I care, but I cannot communicate normally right now.”

### While quiet
“Help me reduce uncertainty without creating another task.”

### When capacity returns
“Help me reconnect without writing a perfect explanation.”

## MVP journeys

See `04-ux-content/01-core-journeys.md` for the full journey. Summary:

### Going Quiet (formerly "Create a Hold")
- select one or more Circles (setup happens inline, not separate onboarding)
- choose message intent
- review
- send (default: text/SMS to everyone; nothing else to do afterwards)

### Reconnect (formerly "Return from Hold")
- persists the audience from Going Quiet by default; add/remove individuals as needed
- tapping Reconnect is a single action (symmetric with Going Quiet) leading into Conversations
- Conversations: per-person, Quick message or Personalise (paste their message, get help wording a reply), tick/untick as complete

### Taking Time
- optional resting state between Going Quiet and Reconnect
- "Send an update" lets the user reassure Circles without ending Taking Time
- "Add to Going Quiet" handles the edge case of a new contact messaging while away

## Message anatomy

A Hold message may include:

1. State
2. Relationship reassurance
3. Boundary
4. Expectation
5. Return signal

Not every message needs every component.

## Explicitly outside MVP

- Reading private WhatsApp or Instagram conversations
- Automatic replies
- Recipient tracking
- Relationship scores
- Social network features
- Clinical assessment
- Crisis triage
- Continuous monitoring
- AI messages sent without review
