# MVP requirements

## P0 — required

### Account and privacy
- Clear onboarding
- Privacy summary in plain language
- Data deletion (previously listed as "Account deletion" — renamed to match the decided account-free model in `04-ux-content/05-onboarding-empty-states.md`: since no account is required, this means a clear, complete way to wipe all local Hold data from the device, plus revoke any optional backup if one was set up)
- Export or delete saved content where applicable

### Hold Circle
- Create, edit and delete circles
- Add contacts manually or through permission-based selection
- Do not upload the full address book by default

### Going Quiet
- Select one or more Circles (inline setup, not separate onboarding)
- Select intent or write from scratch
- Generate or choose a draft
- Edit
- Preview recipients and final text
- Share through native share sheet
- Calm completion state — nothing else to do afterwards

### Taking Time
- Calm resting state; no default reminder to reconnect
- Optional "Send an update" to reassure Circles without ending Taking Time
- Optional "Add to Going Quiet" for a new contact messaging while away

### Reconnect
- Persist audience from Going Quiet by default; allow add/remove per person
- Single-tap action (no upfront choice screen) — leads directly into Conversations
- No overdue language

### Conversations
- Three tiers: Send to everyone (bulk, all Circles) → per-Circle bulk send (different message per Circle) → per person (Quick message or Personalise)
- List grouped by the Circles originally messaged at Going Quiet, not a flat list
- "+ Add person" for new contacts not part of the original Circles, added one at a time
- Confirm step on any bulk action (Tier 1 or Tier 2) to prevent accidental sends
- Tick/untick as complete, always reversible
- Available standalone, not only after a Going Quiet journey
- No counts, unread badges or "outstanding" language

### Safety
- Clear statement that Hold is not emergency or medical support
- Contextual route to urgent support information
- No claims about how recipients will respond

### Accessibility
- Screen-reader labels
- Dynamic text
- Contrast compliance
- Reduced motion
- Usable touch targets

## P1 — after validation

- Optional user-chosen reminders
- Saved personal phrases
- Templates by relationship
- Gentle recipient guidance
- Subscription management
- Anonymous feedback
- Privacy-preserving analytics
