# Design direction

## Emotional brief

Hold should feel:

- held, not managed
- quiet, not empty
- warm, not childish
- hopeful, not falsely cheerful
- premium, not exclusive
- calm, not low-contrast
- simple, not vague

## Layout

- Generous purposeful space
- Clear single-column hierarchy
- One primary action
- Stable navigation
- Minimal visual noise
- No dense home dashboard

## Shape

Soft geometry may support the feeling of being held, but not every component should be rounded.

**Decision (supersedes earlier "circle-being-held" icon direction):** the main interaction circle stays a simple, filled, geometric circle. No open/closed scribble, no split shape, no enclosing "hug" form. That earlier direction read as too soft/whimsical for a product that also needs to feel usable and gender-neutral. State is communicated through scale, opacity/visual weight and surrounding colour, not through the shape opening or closing.

## Icon

The small wordmark logo stays static and unanimated — it's a brand identity element, not a state indicator. Do not apply the motion/state behaviour below to the logo.

## Motion

Core principle: **Action pages are responsive; state pages are restful.**

- User actions get immediate, quick feedback (approx. 200–350ms) — do not delay navigation for a long animation.
- Slower, emotional transitions complete on the following state screen, not before navigation.
- Respect reduced motion — with it enabled, use an immediate or brief crossfade instead of scale/breathing animation.
- No bouncing, confetti or gamified celebration.

### Going Quiet — settling inward
The central circle shrinks to roughly 70–80% of its active size (test 20%, 25%, 30% reductions; store as a design token, not hardcoded) and becomes visually warmer/more weighted. The metaphor is settling and containment, not disappearing or closing off — avoid "offline," "disconnected," "inactive" language or imagery.

### Taking Time — breathing
Once settled, an extremely subtle breathing animation (approx. 98–100% scale over a slow cycle) may run — no pulse, no glow, no obvious rhythm.

### Reconnect — opening outward
The circle gently expands back toward full size. The metaphor is breathing out / sunrise, not "back online." No bounce, spring overshoot or celebration effects.

### Colour environment
Carry the metaphor into the palette: Taking Time uses a subtly warmer, golden-hour-toned background and deeper green across every screen shown in that state; Reconnect gradually returns to the fresh, cooler daytime palette. See `02-colour-and-typography.md` for values.
