# Voice and language

## Hold is

- warm
- quiet
- direct
- adult
- non-clinical
- reassuring
- emotionally precise

## Hold is not

- chirpy
- overly therapeutic
- infantilising
- corporate
- guilt-inducing
- falsely certain

## Recurring language conventions

- No em dashes in any drafted copy. Use commas, full stops, or a rewrite instead. Confirmed on-device with the finalised welcome screen copy.

## Governing voice principle (research-backed)

Informed by lived-experience research on the guilt spiral in chronic illness (see `02-research/06-guilt-spiral-and-supportive-language.md`), and applied everywhere in the app — welcome and first-launch copy, temporary/placeholder wording, transitions, status labels, prompts, notifications:

- **Gentle, short, genuine statements that validate.** Brevity is a feature, not a compromise — short validating lines outperform lengthy reassurance.
- **Permission without pressure, and without commentary.**
- **Never praise the person for a basic act of communication** ("well done" for sending a message reframes communication as an achievement and adds pressure).
- **Never name or narrate the person's psychology back to them** ("this helps your guilt spiral" explains someone to themselves and reads as clinical). Demonstrate understanding by being gentle and asking nothing, rather than stating that you understand.

- Use "your circles" consistently, rather than switching between "your circle," "your people," "your contacts" — one term, used the same way everywhere.
- "Keep your circles in the loop" is the recurring phrase for what Hold does — worth reusing across onboarding, marketing and in-app copy rather than rephrasing it differently each time.
- Avoid copy that implies the user has, or should have, a large support network. "Your circles" should read naturally whether someone has one person in their Close Circle or many — never phrase things in a way that could make a small network feel inadequate.

## Public claims/copy rule: communication framing, not treatment framing

**Logged 2026-08-27, blocked/standing rule, not yet reflected in all copy.** All public-facing copy must describe Hold's function as facilitating communication and connection, never as treating, reducing, or managing a named psychological symptom (e.g. "reduces the shame/guilt spiral," "manages your anxiety"). Applies even where underlying design intent genuinely targets such an outcome (e.g. the guilt-spiral research behind Reconnect, see `02-research/06-guilt-spiral-and-supportive-language.md`). Reasoning: UK medical device classification (MHRA) turns on stated intended purpose/claims, not underlying mechanism. Keeping this framing disciplined is both a legal safeguard and honest to what Hold is — a social support tool, not a clinical intervention.

## "We" — where it belongs and where it doesn't

**Decided:** "we" (the team behind Hold) is reserved for moments where the team is genuinely speaking to the user — the welcome screen, About/Mission content, and feedback requests. It does not appear inside the core journey (Going Quiet, Taking Time, Reconnect, Conversations, transition and completion screens). Those should centre the user and their circles, not Hold-the-company. Within the journey, refer to "Hold" in the third person if the product itself needs naming ("Hold will be here whenever you need it"), not "we."

## Language rules

- Use short sentences.
- Prefer ordinary words.
- Name the action clearly.
- Do not demand optimism.
- Do not imply failure.
- Do not promise a recipient will understand.
- Avoid “should.”
- Avoid “just.”
- Avoid “get back on track.”
- Avoid “you disappeared.”
- Avoid “people are waiting.”
- Avoid excessive exclamation marks.

## Content depth by Circle type — guidance, not enforcement (added 2026-08-11)

Per disclosure-decision-making research (Joachim & Acorn, 2000, *Journal of Advanced Nursing*; the Disclosure Decision-Making Model, Chaudoir & Fisher — see `02-research/07-extended-evidence-base.md`, "Disclosure decision-making," for full citations and the correlational/theoretical tagging of each): how much someone discloses, and how comfortably, tracks closeness with the recipient, and closer relationships tend to receive fuller disclosure more positively. This is **guidance for what Hold suggests by default, not a restriction on what a user can write** — the app never limits or edits what someone actually types, regardless of which Circle it's going to.

Where this applies — template starter suggestions (chips, default messages) and onboarding copy that models what a message might look like:

- **Close/Core Circle** — starter content can be fuller and more personal by default: naming feelings, giving more context, less hedging.
- **Friends** — lighter by default: still warm, less detailed.
- **Work** — most minimal by default: brief, practical, no emotional detail expected. The existing "Work-safe" example below already reflects this instinct; this section makes the underlying reasoning explicit and extends it to template starters and onboarding copy generally, not just that one example message.

This is a starting-point default per Circle type, surfaced as a suggestion — someone can always write more or less than the suggested depth for any Circle, and Hold should never imply one choice is more correct than another.

## Example Hold messages

### Minimal
> I’m low on capacity and may be quiet for a while. I care about you. You don’t need to fix anything.

### No explanation
> I need some quiet time. This isn’t about you, and I’ll reach out when I can.

### Work-safe
> I’m dealing with a period of reduced capacity and may respond more slowly than usual. I’ll follow up when I’m able.

## Example return messages

### Open the door
> I’m starting to resurface. I’m not fully back, but I wanted to say hello.

### Acknowledge time
> I know I’ve been quiet. I cared even when I couldn’t reply. I’d like to reconnect gently.

## Core vocabulary — decided, not open for casual variation

**Added 2026-08-31, from an extended external design/research session (2026-08-19 onward). See `08-decisions/01-decision-log.md`, 2026-08-31.** Checked against this file's existing content first — none of these terms previously appeared here; nothing below overrides prior decisions in this file.

| Term | Meaning | Register |
|---|---|---|
| **On Hold** | The user's own communication status, stated plainly. | Public, outward-facing. |
| **Held** | A recipient's wordless acknowledgement: "received, I respect this, no response needed." | Private, contextual only — see "The 'Held' acknowledgement" below; this must never become a dashboard status. |
| **Holding** | Internal description of a relationship state — this connection is being held without active conversation. | Internal/backend concept only. **Never used publicly to describe a person** ("Bethany is being held") — reads as controlling or clinical, like someone else has authority over them. |
| **Reconnecting** | The user has chosen to open a particular connection at a level that feels possible. | Public to the specific people involved only. |
| **Connection held** | Recipient-facing confirmation after they acknowledge. | Contextual, per-person. |

**"Holding space" may be used once, explained plainly, and then dropped** — a real therapeutic concept (keeping someone in mind without demanding performance or trying to fix them), but it sounds vague or overly therapeutic if used repeatedly without explanation. Suggested one-time explanation: *"Holding a connection means keeping someone in mind without asking them to respond, explain, or return before they're ready."*

This vocabulary, and everything below in this section, is governed by the same reconnection-must-never-be-compulsory requirement as the rest of Reconnect — see `06-privacy-security/07-reconnection-safety-requirements.md`.

## The "Held" acknowledgement — a specific, non-negotiable constraint

**Psychology grounding (Research panel candidate):** the reciprocity norm — unsolicited gestures create a felt pressure to respond, operating below conscious awareness, even when nothing is explicitly requested in return. This risk runs in both directions: a recipient may feel quiet pressure to send "Held" even though it's optional, and the sender must never be able to see acknowledgement status as an aggregated, checkable list.

**Contextual only, never a dashboard.** Acknowledgement status is only ever shown when the user opens that one specific person's connection — never as a list, count, or dashboard. This is the same no-dashboard, no-tally principle already governing the rest of the app (no percentages, no completion rings, no "12 people left") — see `04-ux-content/06-state-architecture-and-memory.md` for the full memory-model rule this belongs to.

**Additional requirements:**
- The user must be able to disable receiving "Held" acknowledgements entirely, if even receiving them creates pressure.
- Acknowledging must never generate a push notification to the sender unless the sender explicitly opted in to that.
- A recipient's failure to send "Held" must carry zero visible consequence anywhere in the sender's experience.

## Language the product should never use

Avoid entirely, in any default/ordinary-return copy: "Make amends." / "Repair the harm." / "Ask for forgiveness." / "Take responsibility." / "People have been waiting." / "Clear your communication debt."

Apology-appropriate language of this kind belongs only in an explicitly opt-in repair pathway, never the default return path — see `02-research/08-cross-cultural-withdrawal-and-repair.md`'s "Formal Reconnect-phase architecture" section for the full Pathway 1 (ordinary return, no wrongdoing presumed) vs. Pathway 2 (optional repair) structure.

## Metaphor families — optional, user-selected, never the only vocabulary

Literal language must always be available as a non-metaphor default. Optional metaphor families a user can select for their own status wording:

- **Weather:** "I'm moving through heavy weather."
- **Seasonal:** "I'm in a quieter season."
- **Tide:** "My social energy is at low tide."
- **Fallow:** "I'm taking a fallow period. I'm not storing up replies for later." (Agriculture grounding: fallow land is deliberately left uncultivated to allow soil fertility to recover — the useful transfer is that a field left fallow isn't *failing* to produce, it's temporarily outside production. Metaphor only, not a scientific claim that human capacity works identically to soil.)
- **Shelter:** "I'm taking shelter for a while."
- **Signal:** "My signal is weak. My care hasn't disappeared."
- **Hearth:** "I'm keeping the connection warm."
- **Orbit:** "I'm further away, but still connected."

A user should be able to save a preferred metaphor family during setup, so Hold can offer language that already feels like theirs when they have little capacity to write something from scratch.

**Choice-load check, per the standing low-capacity design principle (`02-research/02-low-capacity-design.md`):** eight metaphor families is a lot of options to present at once. Present metaphor selection as a low-priority, optional setup step the user can skip entirely (defaulting to literal language), not as a required decision — consider a shorter default subset with "see more" progressive disclosure rather than all eight at once.

**Accessibility:** any interactive element built for this system (the "Held" acknowledgement button, the metaphor-family selector) needs an explicit screen-reader label, not just visible text — particularly the metaphor selector, since metaphor names alone ("Fallow," "Tide") may not be self-explanatory to a screen-reader user without their accompanying description also being announced. All copy in this system supports dynamic text sizing per the existing type-scale rule (`05-design-system/02-colour-and-typography.md`) — no hardcoded text containers that clip or truncate at larger accessibility text sizes.

## "Different clocks"

The absent person may experience an absence as survival compressed into a blur; the waiting person may experience each day as new evidence requiring interpretation. Neither experience is wrong — they're on different relational clocks. Suggested standalone copy, usable on the universal web page (`04-ux-content/07-universal-web-page.md`) or in onboarding:

> "Time can feel different on each side of a pause. A long silence may pass quickly for someone surviving low capacity, and slowly for someone waiting without information."

**Design consequences, apply globally:**
- Never display absence duration as an accusation ("you have kept Sam waiting for 47 days" — do not build anything resembling this).
- Let users hide exact elapsed-time dates if they choose.
- Default return option is always "start from today," never a forced accounting of elapsed time — see `04-ux-content/06-state-architecture-and-memory.md`'s "start from now" principle.

## Research panel candidates — for Settings → Research

Per the existing Settings panel structure (`04-navigation-architecture.md`), suggested short entries (1–2 sentences, not full citations):

- **On the "Held" acknowledgement being contextual-only, never a dashboard:** *"Even a friendly 'received' can create quiet pressure to respond — research on the reciprocity norm shows this happens below conscious awareness, even when nothing is explicitly asked for. Hold never shows who has or hasn't acknowledged, so nobody feels watched or counted."*
- **On avoiding duration/accusation language:** *"Time can feel different on each side of a pause — Hold doesn't display how long you've been away, or how long someone's been waiting, as a number to be judged against."*

Full academic citations stay in `02-research/08-cross-cultural-withdrawal-and-repair.md`; the app only needs the plain-language version.

## Status

Not built in `hold-app` yet — vocabulary, "Held" mechanism, metaphor families, and "different clocks" copy are all reference/spec material for future scoped feature work.
