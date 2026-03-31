# EU5 Game File Structure Guide

This guide maps the game's `/in_game/common/` directory for modding reference.

**Index of Major Systems:**
- [Advances](#advances)
- [Age](#age)
- [AI Diplomatic Chance](#ai-diplomatic-chance)
- [Alert Descriptions](#alert-descriptions) *(UI/Presentation)*
- [Artist Types](#artist-types) *(Data/Reference)*
- [Artist Work](#artist-work)
- [Attribute Columns](#attribute-columns) *(UI/Presentation)*
- [Auto Modifiers](#auto-modifiers)
- [Avatars](#avatars)
- [Armies & Military](#armies--military)
- [Buildings](#buildings)
- [Characters & Traits](#characters--traits)
- [Disasters & Events](#disasters--events)
- [Government & Politics](#government--politics)
- [Modifiers & Effects](#modifiers--effects)
- [Missions & Content](#missions--content)
- [Religion & Culture](#religion--culture)
- [Trade & Economy](#trade--economy)
- [War & Diplomacy](#war--diplomacy)

---

## Index

| System | Folder | Stage |
|---|---|---|
| [Advances](advances.md) | `in_game/common/advances/` | stub |
| [Auto Modifiers](auto_modifiers.md) | `in_game/common/auto_modifiers/` | stub |
| [Buildings](buildings.md) | `in_game/common/building_types/` | stub |
| [Casus Belli](casus_belli.md) | `in_game/common/casus_belli/` | stub |
| [Character Interactions](character_interactions.md) | `in_game/common/character_interactions/` | stub |
| [Disasters](disasters.md) | `in_game/common/disasters/` | stub |
| [Government Reforms](government_reforms.md) | `in_game/common/government_reforms/` | stub |
| [Government Types](government_types.md) | `in_game/common/government_types/` | stub |
| [Laws](laws.md) | `in_game/common/laws/` | stub |
| [Missions](missions.md) | `in_game/common/missions/` | stub |
| [Modifiers](modifiers.md) | `in_game/common/modifiers/` | stub |
| [Policies](policies.md) | `in_game/common/policies/` | stub |
| [Production Methods](production_methods.md) | `in_game/common/production_methods/` | stub |
| [Religions](religions.md) | `in_game/common/religions/` | stub |
| [Scripted Effects](scripted_effects.md) | `in_game/common/scripted_effects/` | stub |
| [Scripted Triggers](scripted_triggers.md) | `in_game/common/scripted_triggers/` | stub |
| [Static Modifiers](static_modifiers.md) | `in_game/common/static_modifiers/` | stub |
| [Subject Types](subject_types.md) | `in_game/common/subject_types/` | stub |
| [Technologies](technologies.md) | `in_game/common/technologies/` | stub |
| [Traits](traits.md) | `in_game/common/traits/` | stub |
| [Unit Types](unit_types.md) | `in_game/common/unit_types/` | stub |
| [War Goals](wargoals.md) | `in_game/common/wargoals/` | stub |

---

## System Entries

## Advances
**Annotation:** [advances.md](advances.md)
**Folder:** `in_game/common/advances/`
**Keywords:**
**Stage:** stub

## Auto Modifiers
**Annotation:** [auto_modifiers.md](auto_modifiers.md)
**Folder:** `in_game/common/auto_modifiers/`
**Keywords:**
**Stage:** stub

## Buildings
**Annotation:** [buildings.md](buildings.md)
**Folder:** `in_game/common/building_types/`
**Keywords:**
**Stage:** stub

## Casus Belli
**Annotation:** [casus_belli.md](casus_belli.md)
**Folder:** `in_game/common/casus_belli/`
**Keywords:**
**Stage:** stub

## Character Interactions
**Annotation:** [character_interactions.md](character_interactions.md)
**Folder:** `in_game/common/character_interactions/`
**Keywords:**
**Stage:** stub

## Disasters
**Annotation:** [disasters.md](disasters.md)
**Folder:** `in_game/common/disasters/`
**Keywords:**
**Stage:** stub

## Government Reforms
**Annotation:** [government_reforms.md](government_reforms.md)
**Folder:** `in_game/common/government_reforms/`
**Keywords:**
**Stage:** stub

## Government Types
**Annotation:** [government_types.md](government_types.md)
**Folder:** `in_game/common/government_types/`
**Keywords:**
**Stage:** stub

## Laws
**Annotation:** [laws.md](laws.md)
**Folder:** `in_game/common/laws/`
**Keywords:**
**Stage:** stub

## Missions
**Annotation:** [missions.md](missions.md)
**Folder:** `in_game/common/missions/`
**Keywords:**
**Stage:** stub

## Modifiers
**Annotation:** [modifiers.md](modifiers.md)
**Folder:** `in_game/common/modifiers/`
**Keywords:**
**Stage:** stub

## Policies
**Annotation:** [policies.md](policies.md)
**Folder:** `in_game/common/policies/`
**Keywords:**
**Stage:** stub

## Production Methods
**Annotation:** [production_methods.md](production_methods.md)
**Folder:** `in_game/common/production_methods/`
**Keywords:**
**Stage:** stub

## Religions
**Annotation:** [religions.md](religions.md)
**Folder:** `in_game/common/religions/`
**Keywords:**
**Stage:** stub

## Scripted Effects
**Annotation:** [scripted_effects.md](scripted_effects.md)
**Folder:** `in_game/common/scripted_effects/`
**Keywords:**
**Stage:** stub

## Scripted Triggers
**Annotation:** [scripted_triggers.md](scripted_triggers.md)
**Folder:** `in_game/common/scripted_triggers/`
**Keywords:**
**Stage:** stub

## Static Modifiers
**Annotation:** [static_modifiers.md](static_modifiers.md)
**Folder:** `in_game/common/static_modifiers/`
**Keywords:**
**Stage:** stub

## Subject Types
**Annotation:** [subject_types.md](subject_types.md)
**Folder:** `in_game/common/subject_types/`
**Keywords:**
**Stage:** stub

## Technologies
**Annotation:** [technologies.md](technologies.md)
**Folder:** `in_game/common/technologies/`
**Keywords:**
**Stage:** stub

## Traits
**Annotation:** [traits.md](traits.md)
**Folder:** `in_game/common/traits/`
**Keywords:**
**Stage:** stub

See: [`advances/`](advances.md) — 100+ files; named by scope (country tag, culture, government type, country type, religion, estate, geography)
Keywords: `advance_id`, `age`, `potential`, `allow`, `requires`, `government`, `country_type`, `for`, `unlock_unit`, `unlock_building`, `unlock_law`, `unlock_levy`, `unlock_government_reform`, `unlock_production_method`, `modifier_while_progressing`

---

## Age

See: [`age/`](../age.md)
Keywords: `age_[id]`, `year`, `price_stability`, `max_price`, `hegemons_allowed`, `efficiency`, `unique`, `modifier`, `mercenaries`, `victory_card`, `war_score_from_battles`, `months_for_exploration_spread`, `max_ai_privilege_per_estate`, `min_ai_privilege_per_estate`

---

## AI Diplomatic Chance

See: [`ai_diplochance/`](ai_diplochance.md)
Keywords: `action_key`, `base`, `opinion`, `trust_in_actor`, `rank_difference`, `different_religion`, `different_culture`, `war_exhaustion`, `in_debt`, `yesman`, `enforced_demand`, `relative_strength`, `border_distance`

---

## Alert Descriptions
**Type: UI / Presentation** — display config only; trigger logic is elsewhere.
See: [`alert_descriptions/`](alert_descriptions.md)
Keywords: `alert_key`, `title`, `texture`, `priority`, `game_concept`

---

## Artist Types
**Type: Data/Reference** — named specializations filtering what art a country can produce.
See: [`artist_types/`](artist_types.md)
Keywords: `artist_type_id`, `potential`

---

## Artist Work
See: [`artist_work/`](artist_work.md)
Keywords: `work_type_id`, `captured`, `allow`, `location_modifier`, `country_modifier`, `religion_scale_modifier`

---

## Attribute Columns
**Type: UI/Presentation** — column layout and sort config for selection lists; tightly coupled to GUI widgets.
See: [`attribute_columns/`](attribute_columns.md)
Keywords: `object_type`, `column_id`, `widget`, `width`, `fixed_height`, `is_constant_width`, `sort`

---

## Auto Modifiers
See: [`auto_modifiers/`](auto_modifiers.md)
Keywords: `modifier_id`, `potential_trigger`, `limit`, `scales_with`, `requires_real`, `hide_effects`, `alert`, `category`, `type`

---

## Avatars
See: [`avatars/`](avatars.md)
Keywords: `avatar_id`, `god`, `potential`, `allow`, `country_modifier`, `location_modifier`, `on_activate`, `on_fully_activated`, `on_deactivate`

## War Goals
**Annotation:** [wargoals.md](wargoals.md)
**Folder:** `in_game/common/wargoals/`
**Keywords:**
**Stage:** stub
