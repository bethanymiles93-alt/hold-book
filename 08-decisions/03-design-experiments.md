# Design experiments

Ideas in this file are **not** product decisions. They align with Hold's philosophy and have plausible benefits, but need user validation before they move into the main product decisions or `01-decision-log.md`.

## Optional Hold signature on template messages

**Status:** Beta hypothesis (not a product decision)

| Why we might do it | Risks | Validation approach |
|---|---|---|
| Gives recipients context for why the message may be shorter or templated. | Some users may feel uncomfortable revealing they are using an app. | Beta test with real users. |
| Introduces Hold naturally through genuine use rather than advertising. | May reduce template adoption if users feel self-conscious. | Measure template usage with signature on/off. |

### Current recommendation

- Make the signature optional.
- Consider showing it only the first time a recipient receives a Hold message.
- Candidate wording:
  - "Sent with love via Hold."
  - "Shared using Hold."

### Design principle

Hold should never require users to advertise the product in order to receive its core benefits. Branding should always be secondary to the user's comfort, privacy and relationships.

### Decision

Remain a beta experiment until validated through user testing.

## Suggesting a Circle addition from usage patterns

**Status:** Beta hypothesis (not a product decision)

If someone repeatedly uses "+ Add person" for the same contact after Going Quiet or during Reconnect, Hold could offer to add them to a saved Circle — e.g. "You've added Jay several times after Going Quiet. Add him to Friends or Core Circle?"

| Why we might do it | Risks | Validation approach |
|---|---|---|
| Saves the user from repeatedly re-adding the same person by hand. | Even phrased as an offer, "I've noticed you..." wording can feel like the app is watching rather than helping — see the same tension already resolved for messaging-mode suggestions. | Beta test the exact wording; measure whether users accept, dismiss or find it unsettling. |

### Current recommendation

- Learning must come entirely from the user's own actions inside Hold (who they've explicitly added), never from message content or external data.
- Frame as an offer the user can decline, not an automatic action.
- Apply the same wording lesson learned elsewhere in this book: prefer "Would you like to add Jay to a Circle?" over "I've noticed you usually add Jay" — the offer, not the observation, should lead.

### Decision

Remain a beta experiment until validated through user testing.
