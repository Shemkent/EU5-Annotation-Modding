# Employment Systems
**Stage:** complete
**Keywords:** employment_system, priority, country_modifier, ai_will_do, building_potential_profit, building_index, capitalism, equality, first_come_first_serve

> **System type: Gameplay**

## Overview
Employment systems determine the order in which buildings across a country receive workers (pops). When total labour demand exceeds supply, the system's `priority` script value ranks buildings — higher scores are staffed first. Each system also grants a country-level modifier while it is active and has an `ai_will_do` block that governs AI selection. In vanilla three core systems exist (equality, first-come-first-served, capitalism) plus a capitalism variant that prioritises infrastructure. The system chosen nudges societal values and shapes which sectors (military, manufacturing, agriculture) get staffed under labour scarcity.

## Vanilla File Locations
- `in_game/common/employment_systems/00_default.txt` — all employment system definitions (one file, 4 systems)
- `in_game/common/employment_systems/readme.txt` — field documentation
- Full file list in `_file_index.csv`.

## Block Structure
```pdx
<employment_system_id> = {
    country_modifier = {
        <modifier_key> = <value>    # modifier applied to the country while this system is active
    }

    priority = {
        <script value>              # root = building; higher score = staffed first
    }

    ai_will_do = {
        <script value>              # root = country; score for AI choosing this system
    }
}
```

## Vanilla Systems
| ID | Priority logic | Country modifier |
|---|---|---|
| `equality` | All buildings equal priority (value = 1) | Monthly push toward communalism |
| `first_come_first_serve` | Oldest buildings filled first (building_index × −1) | Monthly push toward traditional economy |
| `capitalism` | Highest-profit buildings filled first (`building_potential_profit`) | Monthly push toward capital economy |
| `capitalism_prioritising_infrastructure` | Profit-based, but infrastructure/government buildings get +10,000 boost | Minor push toward both capital economy and communalism |

## Key Fields Reference
| Field | Purpose | Key constraint |
|---|---|---|
| `priority` | Script value (root = building) returning a sort score | Higher = staffed earlier; the engine sorts all buildings by this value before assigning workers |
| `country_modifier` | Modifier applied to the country while this system is active | Only one system is active at a time; switching removes the old modifier |
| `ai_will_do` | Score for AI selecting this system | AI picks the highest-scoring system; vanilla uses inertia (−10 base) plus societal value alignment |

## Modding Notes
- **Only one system is active per country at a time.** Switching systems (via laws or events) immediately removes the old `country_modifier` and applies the new one.
- **`priority` runs per building**, not per location. Root is the building being evaluated. Use building-scope script values and conditions — `building_potential_profit`, `building_index`, `building_category`, etc.
- **`ai_will_do` uses societal values** as the primary driver. The `−10` inertia base means the AI will not switch unless societal alignment strongly favours another system. This prevents rapid oscillation.
- **Adding a new employment system** is purely additive — define the block, add localization, and surface the choice via a law or interaction. The engine automatically includes the new system in priority calculations when it is active.
- **Cross-system:** the `country_modifier` from the active employment system stacks with all other country modifiers (laws, government reforms, etc.). Societal value modifiers (e.g. `monthly_towards_capital_economy`) interact with the cultures and societal values systems.

## Example
`capitalism` — staffs the most profitable buildings first:

```pdx
capitalism = {
    country_modifier = {
        monthly_towards_capital_economy = societal_value_monthly_move
    }

    priority = {
        value = building_potential_profit   # script value: expected profit of this building
    }

    ai_will_do = {
        add = {
            desc  = "inertia"
            value = -10                     # base inertia discourages switching
        }
        add = {
            desc  = "societal_values"
            value = societal_value:capital_economy_vs_traditional_economy
            multiply = -1                   # negative of capital_vs_traditional → higher when traditional
        }
    }
}
```

When capitalism is active, labour fills the highest-earning buildings first, leaving low-profit agriculture understaffed under scarcity. The AI switches to capitalism when the societal value `capital_economy_vs_traditional_economy` pulls negative (i.e. the country leans traditional, making capitalism the contrarian push).
