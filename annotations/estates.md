# Estates System
**Stage:** annotated
**Game version:** 1.1.10
**Keywords:** estates, estate_privileges, power_per_pop, tax_per_pop, satisfaction, high_power, low_power, privilege, can_revoke

---

## Overview

Estates are political factions within a country (nobles, clergy, burghers, peasants, etc.). Each estate has:
- **Power** — determined by pop counts and privileges; drives scaled modifiers
- **Satisfaction** — drives approval-based modifiers
- **Opinion** — multi-factor diplomatic opinion calculation (used for foreign estate relations)

**Estate privileges** are specific grants to an estate that apply country/province/location modifiers while active. A country can hold many privileges at once; each privilege belongs to one estate.

---

## File Locations

| Path | Purpose |
|---|---|
| `in_game/common/estates/00_default.txt` | All estate type definitions |
| `in_game/common/estate_privileges/` | All privilege definitions, split by estate |
| `in_game/common/estate_privileges/readme.txt` | Privilege attribute reference |

---

## Estate Definition Syntax

```
estate_key = {
    # --- Presentation ---
    color = <color_key>                     # Map/UI color.

    # --- Power calculation ---
    power_per_pop = <int>                   # Power gained per 1000 pops of this estate type.
    tax_per_pop   = <int>                   # Tax income per 1000 pops.

    # --- Diplomacy ---
    rival    = <float>                      # Opinion modifier per estate rival.
    alliance = <float>                      # Opinion modifier per estate ally.

    revolt_court_language = <language_key>  # Language used in revolts from this estate.

    # --- Character generation ---
    characters_have_dynasty = always|sometimes|never
    can_spawn_random_characters = yes/no
    can_generate_mercenary_leaders = yes/no
    bank = yes/no                           # Can this estate loan money?

    ruler = yes                             # Crown estate only — marks this as the ruler estate.
    priority_for_dynasty_head = yes         # Prioritize when calculating dynasty head.

    # --- Scaled modifiers (multiplied by satisfaction above LOW_SATISFACTION_THRESHOLD) ---
    satisfaction = { <modifiers> }

    # --- Scaled modifiers (multiplied by (power - LOW_POWER_THRESHOLD) when power is high) ---
    high_power = { <modifiers> }

    # --- Scaled modifiers (multiplied by -(power - LOW_POWER_THRESHOLD) when power is low) ---
    low_power = { <modifiers> }

    # --- Power-based modifiers (always active, scaled by power level) ---
    power = { <modifiers> }

    # --- Inter-estate opinion calculation ---
    opinion = {
        add = {
            desc = <loc_key>
            value = <scripted_maths>
        }
        # ... multiple add blocks
    }
}
```

---

## Vanilla Estates

| Key | Pop type | Notes |
|---|---|---|
| `crown_estate` | Ruler | Special ruler estate; `ruler = yes`; power_per_pop = 0 |
| `nobles_estate` | Nobles | Characters have dynasties; generates mercenary leaders |
| `clergy_estate` | Clergy | Characters may have dynasties; no mercenary leaders |
| `burghers_estate` | Burghers | Characters may have dynasties; has bank |
| `peasants_estate` | Peasants | No dynasty; no mercenary leaders |
| `dhimmi_estate` | Dhimmi pops | Religion-based minority estate |
| `cossacks_estate` | Cossacks | Region-specific; military-focused |
| `tribes_estate` | Tribal pops | Tribal governments |

---

## Estate Privilege Syntax

```
privilege_key = {
    estate = <estate_key>           # Required. Which estate this privilege belongs to.

    # --- Availability ---
    potential  = { <triggers> }     # Root = country. Whether the privilege is visible.
    allow      = { <triggers> }     # Root = country. Whether the privilege can be enacted.
    can_revoke = { <triggers> }     # Root = country. Whether the privilege can be revoked.

    # --- Timing ---
    years   = <int>
    months  = <int>
    weeks   = <int>
    days    = <int>

    # --- Effects ---
    on_activate        = { <effects> }
    on_fully_activated = { <effects> }
    on_deactivate      = { <effects> }

    # --- Modifiers ---
    country_modifier  = { <modifiers> }
    province_modifier = { <modifiers> }
    location_modifier = { <modifiers> }
}
```

---

## Power and Satisfaction Mechanics

Estate power and satisfaction drive the scaled modifiers:
- `high_power` modifiers are multiplied by `(power - LOW_POWER_THRESHOLD)` when power > threshold.
- `low_power` modifiers are multiplied by `-(power - LOW_POWER_THRESHOLD)` when power < threshold (penalty).
- `satisfaction` modifiers are multiplied by `(satisfaction - LOW_SATISFACTION_THRESHOLD)` when satisfaction > threshold.

---

## Examples

### 1. Estate definition excerpt (clergy)
```
clergy_estate = {
    color = pop_clergy
    power_per_pop = 10
    tax_per_pop = 25
    rival = -0.01
    alliance = 0.01
    revolt_court_language = liturgical_language
    characters_have_dynasty = sometimes
    bank = yes

    satisfaction = {
        research_speed_modifier = 0.5
        diplomatic_reputation = 2
    }

    high_power = {
        # Benefits when clergy is strong
    }

    low_power = {
        # Penalties when clergy is weak
    }
}
```

### 2. Simple privilege
```
nobles_land_rights = {
    estate = nobles_estate
    country_modifier = {
        nobles_estate_target_satisfaction = medium_privilege_target_satisfaction
        global_nobles_estate_power = 0.75
        global_peasant_enfranchisment = -0.10
        nobles_estate_allowed_to_build_rgo = yes
        monthly_towards_serfdom = societal_value_monthly_move
    }
}
```

### 3. Gated privilege with revoke condition
```
auxilium_et_consilium = {
    estate = nobles_estate
    potential = { government_type = government_type:monarchy }
    allow = {
        has_advance = noble_knights
        NOT = { has_estate_privilege = estate_privilege:monetary_fiefs }
    }
    can_revoke = {}
    country_modifier = {
        global_nobles_estate_power = 0.5
        levy_combat_efficiency_modifier = 0.10
        nobles_estate_levy_size = 0.20
    }
}
```
`can_revoke = {}` — empty trigger means always revocable.

---

## Modding Notes

- New estates: add a block to `estates/00_default.txt`. Requires corresponding pop type, localization, and icons.
- New privileges: add to the appropriate estate's file in `estate_privileges/`, or create a new file.
- Privileges are referenced as `estate_privilege:<privilege_key>` in triggers (e.g. `has_estate_privilege = estate_privilege:nobles_land_rights`).
- `country_modifier` on privileges supports the scaled+triggered form (see laws.md / government_reforms.md for syntax).
- Enacting a privilege usually grants satisfaction to the estate — set this via `nobles_estate_target_satisfaction` or equivalent modifier keys.
