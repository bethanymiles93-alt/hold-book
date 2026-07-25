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
- Two dropdowns, not one progressively-revealing section: Quick message (top, bulk/instant) and Personalise/Conversations (second, per-person AI-assisted)
- Quick message: Circle selection row ("All" first) plus shared message box by default; per-Circle boxes only once "All" breaks
- Unticking someone from Quick message moves them to the Personalise/Conversations dropdown, not a third nested tier
- Sent-state pill: soften/desaturate + checkmark, no selection halo; status label "Sent. They know you're thinking of them." immediately, becomes the date from the next calendar day onward
- Reconnect screen has three actions (Send, Edit, Personalise); Conversations hidden until an instant message is sent or Personalise tapped, then "Want to reply to anyone properly? / Not now" gate
- "+ Add person" for new contacts not part of the original Circles, added one at a time, lands in Personalise/Conversations
- Confirm step on any Quick message bulk action to prevent accidental sends
- Tick/untick as complete, always reversible, never auto-triggered by sending
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
