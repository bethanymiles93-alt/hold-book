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
- One single screen, no separate Review step — select one or more Circles (inline setup, not separate onboarding), select intent or write from scratch, generate or choose a draft, edit
- Per-Circle, per-person include/exclude/remove via a selection-circle control, matching Home's main action-circle visual language
- Personalise routes an excluded person to Conversations instead of an inline compose, seeded only once Send fires
- Send fires the group and individual instant messages together and starts Taking Time; email out-of-office and wider-world status appear after Send as an optional unwind, not before it
- Share through native share sheet
- Calm completion state — one explicit final action ("Done"), nothing automatic

### Taking Time
- Calm resting state; no default reminder to reconnect
- Optional "Send an update" to reassure Circles without ending Taking Time — multi-select Circle chip row, one shared message box, per-Circle sent state persisting for the current Taking Time period only
- Optional "Add to Going Quiet" for a new contact messaging while away

### Reconnect
- Persist audience from Going Quiet by default; allow adding a new person (e.g. via "Add to Going Quiet")
- Single-tap action (no upfront choice screen) — leads directly into a multi-select "All" + per-Circle/per-individual picker sharing one message box
- Completion gate: everyone in the audience must be reached at least once, across as many separate sends as needed, before Personalise/"Not now" and the OOO/status-off controls unlock
- Coverage persists durably (survives force-quit), not just in memory — Home resumes an interrupted session in place rather than losing track of who's been reached
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
