# Ecological Depletion — Design Document

## Intent

EU5 treats land as a passive, inexhaustible backdrop. Production is a function of population + development + buildings. There is no soil, no forest, no watershed — just an abstracted output number. This mod makes the land a finite, degradable resource with real consequences for overexploitation.

Philosophically inspired by Daniel Quinn's Ishmael trilogy: the Taker story assumes the world exists as a resource for human use. This mod makes the cost of that assumption visible and mechanical.

## Current EU5 Behavior

- Geography sets a production maximum loosely tied to terrain type
- Technology and development increase output without limit
- No degradation, no carrying capacity, no feedback loop from extraction to land quality
- A province produces the same goods forever at whatever rate development dictates

## Proposed Mechanic

### Core Loop

1. **Carrying Capacity**: Each province has an ecological carrying capacity derived from its geography (terrain type, climate, latitude). This is the sustainable yield ceiling.

2. **Development Intensity**: Technology controls how close to (and how far beyond) the carrying capacity a province can be pushed. Early tech = low ceiling and low overproduction risk. Industrial tech = high potential yield but catastrophic overproduction capacity.

3. **Overproduction**: When actual output exceeds sustainable yield, a cumulative "Depletion" modifier accrues monthly. This erodes production efficiency gradually.

4. **Threshold Shifts**: When depletion exceeds a threshold, the province undergoes an irreversible (or very slow-recovering) production type shift:
   - Dense Forest -> Sparse Forest -> Scrubland -> Degraded Land
   - Rich Soil -> Depleted Soil -> Eroded Terrain
   - Productive Fishery -> Depleted Fishery -> Barren Coast

5. **Cascading Effects**: One resource collapse can trigger others. No forest -> erosion -> lower agriculture -> famine -> population collapse.

### What Controls Overproduction (Starting Implementation)

Development level vs. terrain capacity. If a province's development rating exceeds what its terrain type naturally supports, overproduction kicks in. This uses existing game data and requires the least new infrastructure.

### Technology Reframing

Technology primarily controls the intensity of development possible:
- Early tech: low sustainable yield AND low overproduction capacity (can't destroy the land quickly)
- Mid tech: moderate sustainable yield, moderate overproduction risk
- Late/industrial tech: high sustainable yield possible, but the gap between extractable output and sustainable output widens dramatically

## Open Questions

- Exact depletion rate scaling — needs playtesting
- Visual feedback for depletion (map mode? terrain tint?)
- Recovery mechanics — how slow? Should some shifts be truly permanent?
- Interaction with trade goods system — does a terrain shift change what goods a province produces?
- How does population pressure feed into overproduction (future enhancement vs. starting scope)?

## Implementation Notes

Key game files to investigate:
- `common/static_modifiers/` — provincial modifiers
- `common/auto_modifiers/` — conditional modifier triggers
- `common/advances/` — technology effects on production
- Terrain and province definition files for carrying capacity baseline
