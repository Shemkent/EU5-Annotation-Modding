# Scripted Triggers
**Stage:** annotated
**Game version:** 1.1.10
**Keywords:** scripted_triggers, reusable triggers, arguments, $variable$, custom_description, trigger_if, trigger_else

---

## Overview

Scripted triggers are named, reusable trigger blocks. They allow complex or repeated trigger logic to be defined once and called anywhere in the script with `my_trigger = yes`. They support parameterized arguments and scope references — same mechanics as scripted_effects.

---

## File Locations

| Path | Purpose |
|---|---|
| `in_game/common/scripted_triggers/` | All scripted trigger definitions |
| `in_game/common/scripted_triggers/readme.txt` | Format reference |

### File organisation (by scope/theme)

| File | Scope/theme |
|---|---|
| `country_triggers.txt` | Country-scoped triggers |
| `character_triggers.txt` | Character-scoped triggers |
| `location_triggers.txt` | Location-scoped triggers |
| `province_triggers.txt` | Province-scoped triggers |
| `pop_triggers.txt` | Pop-scoped triggers |
| `unit_triggers.txt` | Army/navy unit triggers |
| `war_triggers.txt` | War/combat triggers |
| `goods_triggers.txt` | Goods market triggers |
| `culture_triggers.txt` | Culture triggers |
| `religion_triggers.txt` | Religion triggers |
| `building_triggers.txt` | Building triggers |
| `disaster_triggers.txt` | Disaster end/start triggers |
| `cabinet_triggers.txt` | Cabinet triggers |
| `game_triggers.txt` | Global game state triggers |
| `exploration_triggers.txt` | Exploration triggers |
| `international_organization_triggers.txt` | IO triggers |
| `resolution_triggers.txt` | Resolution triggers |
| `situation_triggers.txt` | Situation triggers |
| `work_of_art_triggers.txt` | Artwork triggers |
| `00_event_illustration_triggers.txt` | Event illustration triggers |
| `00_clothing_triggers.txt` | Clothing/appearance triggers |

---

## Syntax

### Simple trigger
```
my_trigger = {
    stability > 5
    prestige > 50
}
```
**Usage:** `my_trigger = yes`

### Parameterized trigger
```
my_argument_trigger = {
    prestige >= $value$
}
```
**Usage:** `my_argument_trigger = { value = 50 }`

### Scoped argument trigger
```
my_scoped_trigger = {
    $target$ = {
        prestige >= $value$
    }
    is_enemy_of = $target$
}
```
**Usage:** `my_scoped_trigger = { target = scope:ally  value = 50 }`

### Type-switched via argument concatenation
```
my_trigger_hello = { always = no }
my_trigger = { my_trigger_$type$ = yes }
```
**Usage:** `my_trigger = { type = hello }`

---

## custom_description Warning

Same as scripted_effects: do **not** use the same key for the trigger and its `custom_description`. Use a distinct `text` key:
```
# BAD:
my_trigger = { custom_description = { text = my_trigger  object = ... } }

# GOOD:
my_trigger = { custom_description = { text = my_trigger_text  object = ... } }
```

---

## Examples

### 1. Reusable country rank check
```
country_rank_is_empire = {
    country_rank_is_what = { target_rank = country_rank:rank_empire }
}

country_rank_is_what = {
    trigger_if = {
        limit = {
            exists = scope:character
            has_ruler = yes
        }
        "country_rank_on_date(scope:character.rule_end_date(root))" ?= $target_rank$
    }
    trigger_else = {
        country_rank ?= $target_rank$
    }
}
```
`trigger_if` / `trigger_else` allow conditional logic within a scripted trigger.

### 2. Estate eligibility check
```
country_can_ennoble_trigger = {
    OR = {
        NOR = {
            government_type = government_type:republic
            government_type = government_type:theocracy
        }
        AND = {
            government_type = government_type:republic
            has_reform = government_reform:noble_elite
        }
    }
}
```
Used as `country_can_ennoble_trigger = yes` in `allow` or `potential` blocks throughout the script.

---

## Modding Notes

- All `.txt` files in `scripted_triggers/` are loaded — add new files freely.
- Arguments are text replacements, not typed variables.
- `trigger_if` / `trigger_else` within a scripted trigger allow branching logic.
- Scripted triggers used as end conditions for disasters (see [disasters.md](disasters.md)) are typically in `disaster_triggers.txt`.
- Scripted triggers are called like any other trigger: `my_trigger = yes` (no args) or `my_trigger = { key = value }` (with args).
