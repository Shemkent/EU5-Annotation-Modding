# Societal Values — Design Document

## Intent

EU5's societal values primarily interact with legal and political institutions rather than the population and their beliefs. Culture is a tag, not a living system. This mod introduces value identities to population cultures, making worldview a mechanical force that shapes governance, extraction, assimilation, and inter-cultural dynamics.

Inspired by Daniel Quinn's concept of "Mother Culture" — the way a civilization's story propagates through populations not by decree but by gradual absorption.

## Current EU5 Behavior

- Population divided into classes (commoners, burghers, clergy, nobility) with needs and contributions
- Societal values shape what laws and institutions are available — primarily a state-level mechanic
- Culture is a population attribute but has thin mechanical impact beyond acceptance status
- No modeling of worldview, cosmological orientation, or value compatibility between cultures and states

## Proposed Mechanic

### Phase 1: Buff Existing Values

Amplify the mechanical impact of EU5's existing societal values, especially on population behavior rather than just institutional unlocks. Audit current values, identify which are underpowered relative to their narrative weight, and increase their effects.

### Phase 2: Culture Value Initialization

Cultures start with a set of values based on:
1. The values of the nation with the largest accepted-culture population at game start
2. If no nation exists for that culture, fall back to the average of the culture group
3. Further fallback to other contextual sources (religion, geography)

### Phase 3: Bidirectional Convergence

- **Culture -> Nation direction**: Culture internal values gradually converge with the values of the nation holding the largest accepted-culture population
- **Nation -> Culture direction**: Nation values gradually move toward the weighted average of its accepted cultures, weighted by political power
- **Exclusion**: Non-accepted cultures do not participate in this convergence process. Their values freeze relative to the nation and diverge over time organically.

### Phase 4: Value Differential Friction

All cultures carry a value differential vs. the nation they live in. This differential creates mechanical friction:
- **Tax/extraction efficiency penalty** scaled to differential magnitude
- **Labor productivity penalty** — populations with sufficiency-oriented values don't respond to accumulation-oriented incentives
- **Conversion resistance** — high value differential makes cultural assimilation harder because the nation's story is less legible
- **Disengagement** — not rebellion, but non-participation. Different from unrest.

The most important framing: sufficiency-oriented populations aren't *resisting* — they're operating by different logic entirely.

### Proposed Value Axes

- **Cosmology**: Animist <-> Monotheist (relationship to the non-human world)
- **Surplus**: Sufficiency-oriented <-> Accumulation-oriented (having enough vs. having more)
- **Kinship**: Communal obligation <-> Individual property (ownership and duty)
- **Time**: Cyclical/ancestral <-> Progressive/future-oriented (tradition vs. improvement)

These are population-level attributes, not nation-level. This allows:
- A Christian kingdom with animist-coded rural peasants (historically accurate for medieval Europe)
- Indigenous populations resistant to colonial labor extraction through value incompatibility, not rebellion mechanics
- Urbanizing populations shifting along the surplus axis as markets integrate — emergent, not decreed

## Open Questions

- Convergence speed calibration — slow enough for 1-2 significant shifts per campaign, not dozens
- Exact mechanical effects per unit of value differential
- How do value axes interact with existing EU5 religion and culture mechanics?
- Should value differential affect military service willingness?
- UI representation — how does the player see culture values and differentials?

## Implementation Notes

Key game files to investigate:
- Culture and culture group definitions
- Societal value definitions and their current effects
- Population modifier systems
- Acceptance mechanics
- Political power weighting systems
