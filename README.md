# The Hold Book

**Owner:** Bethany Miles  
**Status:** Living product source of truth  
**Version:** 0.1

Hold helps people protect meaningful relationships during periods when illness, grief, burnout or overwhelm temporarily reduces their capacity to communicate.

## Product promise

- **Before:** Your people know.
- **During:** You can rest.
- **After:** Hold helps you return.

## Core problem

Hold is not primarily solving a writing problem. It is reducing **relationship erosion caused by temporary loss of capacity**.

The common loop is:

1. Capacity drops.
2. A message feels too difficult.
3. Silence begins.
4. Guilt increases.
5. Returning feels harder.
6. Silence is interpreted as disinterest, rejection or unreliability.
7. Trust and closeness erode.

## Repository map

- `01-foundation/` — mission, problem, principles and founder insight
- `02-research/` — evidence and research implications
- `03-product/` — users, MVP, roadmap (`05-roadmap.md`), requirements and Patterns
- `04-ux-content/` — journeys, navigation architecture, onboarding/empty states, language and notifications
- `05-design-system/` — accessibility, colour, typography and interaction
- `06-privacy-security/` — privacy, AI, safeguarding and safety
- `07-business/` — positioning, pricing, launch and business strategy
- `08-decisions/` — decision log, rejected ideas, design experiments and open questions
- `09-research/` — background research references (e.g. accreditation pathways, international/AI/online-safety compliance scans) not tied to a specific decision or open question

## The Hold Test

A feature should not ship unless it can answer “yes” to the relevant questions:

- Does it reduce guilt or emotional effort?
- Does it preserve or repair human connection?
- Does it increase trust?
- Does it preserve user choice?
- Can someone use it at very low capacity?
- Is the data collected genuinely necessary?
- Can the interaction be explained in plain language?
- Would we still be comfortable with it if engagement metrics were removed?

## Documentation labels

Each page should distinguish:

- **Evidence** — supported by external research or standards
- **Founder insight** — grounded in lived experience
- **Hypothesis** — plausible but not yet validated
- **Decision** — what Hold will do now
- **Test** — what must be learned from users

## Keeping this book in sync with what's built

**A decision-log entry and a hold-book documentation update are two separate questions — answering one never answers the other.** Added 2026-09-01, after an audit found real, shipped features (Going Quiet/Reconnect's per-Circle last-sent-message preview, Conversations' own per-person version) with zero mentions anywhere in this book, months after being built — both had been correctly judged as "not a new product decision, just implementing a given spec," which is a true answer to the wrong question.

Before considering a build task finished, check both, separately:

1. **Does this need a new `08-decisions/01-decision-log.md` row?** Only if it's a new or revised product/design decision — not every implementation detail needs one.
2. **Does the feature itself need documenting somewhere in this book, findable later?** Almost always yes, for anything that's a real user-facing feature or screen behaviour — regardless of whether it was a "new decision" or "just building an already-given spec." A feature can be a correct, spec-following build and still be completely undocumented; those are two separate gaps, and "it was just implementing spec" only ever answers the first question, never the second.

When in doubt about (2), document it — a page that's slightly more detailed than strictly necessary costs a future reader a few seconds; a real feature with no page describing it costs a future reader (or a future session working from this book) having to rediscover it from the code, or worse, treating on-device confirmation of it as confusion, forgotten work, or a regression when it was neither.
