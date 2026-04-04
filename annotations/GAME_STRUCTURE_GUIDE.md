# EU5 Game File Structure Guide

Covers `in_game/common/` (115 folders) and `main_menu/common/` (14 entries).
Annotation status is kept in `_file_index.csv`. This guide is the roadmap — it shows what exists, how folders cluster, and what to prioritize.

---

## Priority Tiers

**Tier 1 — Core gameplay** *(annotate first)*
Buildings, laws, government types & reforms, advances, religions, traits, technologies, production methods, disasters, estates & privileges, scripted effects & triggers, modifiers

**Tier 2 — Diplomacy & war**
Casus belli, wargoals, peace treaties, subject types, international organizations, country interactions, generic actions

**Tier 3 — Economy & population**
Goods, prices, goods demand, pop types, levies, employment systems, production methods, policies

**Tier 4 — Characters & culture**
Character interactions, child educations, cultures, culture groups, societal values, traits, trait flavor, ethnicities, genes

**Tier 5 — Religion**
Religions, religion groups, religious aspects/factions/figures/focuses/schools, gods, holy sites, avatars

**Tier 6 — Scripted infrastructure**
Script values, scripted lists, scripted modifiers, scripted rules, scripted geography, scripted relations, scripted country names, scripted diplomatic objectives, on_action, scripted_guis, scripted_hints, trigger/effect localization

**Tier 7 — AI**
AI diplomatic chance, biases, rival criteria, generic action AI lists, join war rules

**Tier 8 — UI / Presentation / Niche**
Alert descriptions, attribute columns, artist types & work, insults, death reason, designated heir reason, customizable localization, music player tracks, tutorial lessons, road types, topography, vegetation, climates, town setups, location ranks, country ranks, historical scores, persistent DNA

---

## Domain Clusters

### Government & Politics
| Folder | Likely System | Stage |
|---|---|---|
| `in_game/common/government_types/` | government_types | annotated |
| `in_game/common/government_reforms/` | government_reforms | annotated |
| `in_game/common/laws/` | laws | annotated |
| `in_game/common/policies/` | policies | stub |
| `in_game/common/cabinet_actions/` | government_types | unmapped |
| `in_game/common/parliament_types/` | government_types | unmapped |
| `in_game/common/parliament_agendas/` | government_types | unmapped |
| `in_game/common/parliament_issues/` | government_types | unmapped |
| `in_game/common/regencies/` | government_types | unmapped |
| `in_game/common/resolutions/` | government_types | unmapped |
| `in_game/common/hegemons/` | government_types | unmapped |
| `in_game/common/formable_countries/` | government_types | unmapped |
| `in_game/common/country_ranks/` | government_types | unmapped |
| `main_menu/common/game_rules/` | game_rules | unmapped |
| `main_menu/common/scenarios/` | scenarios | unmapped |

### Military & War
| Folder | Likely System | Stage |
|---|---|---|
| `in_game/common/unit_types/` | unit_types | stub |
| `in_game/common/unit_categories/` | unit_types | unmapped |
| `in_game/common/unit_abilities/` | unit_types | unmapped |
| `in_game/common/unit_formation_preference/` | unit_types | unmapped |
| `in_game/common/levies/` | levies | unmapped |
| `in_game/common/recruitment_method/` | levies | unmapped |
| `in_game/common/wargoals/` | wargoals | annotated |
| `in_game/common/casus_belli/` | casus_belli | annotated |
| `in_game/common/peace_treaties/` | wargoals | annotated |
| `in_game/common/join_war_rules/` | wargoals | annotated |
| `in_game/common/subject_military_stances/` | subject_types | unmapped |

### Diplomacy & International
| Folder | Likely System | Stage |
|---|---|---|
| `in_game/common/subject_types/` | subject_types | annotated |
| `in_game/common/international_organizations/` | international_organizations | annotated |
| `in_game/common/international_organization_payments/` | international_organizations | annotated |
| `in_game/common/international_organization_land_ownership_rules/` | international_organizations | annotated |
| `in_game/common/international_organization_special_statuses/` | international_organizations | annotated |
| `in_game/common/country_interactions/` | country_interactions | annotated |
| `in_game/common/generic_actions/` | generic_actions | annotated |
| `in_game/common/generic_action_ai_lists/` | ai_generic_actions | unmapped |
| `in_game/common/diplomatic_costs/` | country_interactions | annotated |
| `in_game/common/scripted_diplomatic_objectives/` | scripted_diplomatic_objectives | unmapped |
| `in_game/common/scripted_relations/` | scripted_relations | unmapped |
| `in_game/common/rival_criteria/` | ai_rivals | unmapped |
| `in_game/common/insults/` | country_interactions | annotated |
| `in_game/common/situations/` | situations | unmapped |

### Economy & Trade
| Folder | Likely System | Stage |
|---|---|---|
| `in_game/common/goods/` | goods | annotated |
| `in_game/common/prices/` | goods | annotated |
| `in_game/common/goods_demand/` | goods | annotated |
| `in_game/common/goods_demand_category/` | goods | annotated |
| `in_game/common/production_methods/` | production_methods | annotated |
| `in_game/common/building_types/` | buildings | annotated |
| `in_game/common/building_categories/` | buildings | annotated |
| `in_game/common/pop_types/` | pop_types | annotated |
| `in_game/common/employment_systems/` | employment_systems | annotated |
| `in_game/common/policies/` | policies | annotated |

### Estates & Characters
| Folder | Likely System | Stage |
|---|---|---|
| `in_game/common/estates/` | estates | annotated |
| `in_game/common/estate_privileges/` | estates | annotated |
| `in_game/common/character_interactions/` | character_interactions | annotated |
| `in_game/common/child_educations/` | child_educations | annotated |
| `in_game/common/heir_selections/` | heir_selections | annotated |
| `in_game/common/traits/` | traits | annotated |
| `in_game/common/trait_flavor/` | traits | annotated |
| `in_game/common/genes/` | genes | unmapped |
| `in_game/common/persistent_dna/` | genes | unmapped |
| `in_game/common/ethnicities/` | ethnicities | unmapped |

### Technology & Progression
| Folder | Likely System | Stage |
|---|---|---|
| `in_game/common/advances/` | advances | stub |
| `in_game/common/technologies/` | technologies | n/a — folder absent in v1.1.10; see advances |
| `in_game/common/age/` | age | complete |
| `in_game/common/institution/` | institutions | unmapped |
| `in_game/common/disasters/` | disasters | annotated |
| `in_game/common/missions/` | missions | stub |
| `in_game/common/mission_task_defs/` | missions | unmapped |
| `main_menu/common/achievements/` | achievements | unmapped |
| `main_menu/common/achievement_groups.txt` | achievements | unmapped |
| `main_menu/common/scenarios/` | scenarios | unmapped |

### Religion & Culture
| Folder | Likely System | Stage |
|---|---|---|
| `in_game/common/religions/` | religions | annotated |
| `in_game/common/religion_groups/` | religions | annotated |
| `in_game/common/religious_aspects/` | religious_aspects | annotated |
| `in_game/common/religious_factions/` | religious_schools | annotated |
| `in_game/common/religious_figures/` | religious_schools | annotated |
| `in_game/common/religious_focuses/` | religious_focuses | annotated |
| `in_game/common/religious_schools/` | religious_schools | annotated |
| `in_game/common/gods/` | gods | annotated |
| `in_game/common/holy_site_types/` | holy_sites | annotated |
| `in_game/common/holy_sites/` | holy_sites | annotated |
| `in_game/common/avatars/` | avatars | complete |
| `in_game/common/culture_groups/` | cultures | annotated |
| `in_game/common/cultures/` | cultures | annotated |
| `in_game/common/societal_values/` | societal_values | annotated |
| `in_game/common/language_families/` | languages | annotated |
| `in_game/common/languages/` | languages | annotated |

### Modifiers & Effects (Scripted Infrastructure)
| Folder | Likely System | Stage |
|---|---|---|
| `in_game/common/modifiers/` | modifiers | annotated (conceptual guide, no single folder) |
| `in_game/common/static_modifiers/` | static_modifiers | n/a — folder absent in v1.1.10 |
| `in_game/common/auto_modifiers/` | auto_modifiers | annotated |
| `in_game/common/scripted_modifiers/` | scripted_modifiers | annotated |
| `in_game/common/scripted_effects/` | scripted_effects | annotated |
| `in_game/common/scripted_triggers/` | scripted_triggers | annotated |
| `in_game/common/scripted_rules/` | scripted_rules | unmapped |
| `in_game/common/script_values/` | script_values | unmapped |
| `in_game/common/scripted_lists/` | scripted_lists | unmapped |
| `in_game/common/on_action/` | on_action | unmapped |
| `in_game/common/scriptable_hints/` | scriptable_hints | unmapped |
| `in_game/common/scripted_guis/` | scripted_guis | unmapped |
| `in_game/common/scripted_country_names/` | scripted_country_names | unmapped |
| `in_game/common/scripted_geography/` | scripted_geography | unmapped |
| `in_game/common/effect_localization/` | effect_localization | unmapped |
| `in_game/common/trigger_localization/` | trigger_localization | unmapped |
| `in_game/common/customizable_localization/` | customizable_localization | unmapped |
| `main_menu/common/static_modifiers/` | static_modifiers | unmapped |
| `main_menu/common/scripted_triggers/` | scripted_triggers | unmapped |
| `main_menu/common/scripted_lists/` | scripted_lists | unmapped |
| `main_menu/common/script_values/` | script_values | unmapped |
| `main_menu/common/modifier_type_definitions/` | modifiers | unmapped |
| `main_menu/common/modifier_icons/` | modifiers | unmapped |

### AI
| Folder | Likely System | Stage |
|---|---|---|
| `in_game/common/ai_diplochance/` | ai_diplochance | complete |
| `in_game/common/biases/` | ai_biases | unmapped |
| `in_game/common/rival_criteria/` | ai_rivals | unmapped |
| `in_game/common/generic_action_ai_lists/` | ai_generic_actions | unmapped |
| `in_game/common/join_war_rules/` | ai_war | unmapped |

### Geography & Map
| Folder | Likely System | Stage |
|---|---|---|
| `in_game/common/climates/` | map_geography | unmapped |
| `in_game/common/topography/` | map_geography | unmapped |
| `in_game/common/vegetation/` | map_geography | unmapped |
| `in_game/common/road_types/` | map_geography | unmapped |
| `in_game/common/location_ranks/` | map_geography | unmapped |
| `in_game/common/town_setups/` | map_geography | unmapped |
| `in_game/common/scripted_geography/` | scripted_geography | unmapped |

### UI / Presentation / Data
| Folder | Likely System | Stage |
|---|---|---|
| `in_game/common/alert_descriptions/` | alert_descriptions | complete |
| `in_game/common/attribute_columns/` | attribute_columns | complete |
| `in_game/common/artist_types/` | artist_types | complete |
| `in_game/common/artist_work/` | artist_work | complete |
| `in_game/common/music_player_tracks/` | music_player_tracks | unmapped |
| `in_game/common/tutorial_lesson_chains/` | tutorial | unmapped |
| `in_game/common/tutorial_lessons/` | tutorial | unmapped |
| `in_game/common/historical_scores/` | historical_scores | unmapped |
| `in_game/common/country_description_categories/` | ui_data | unmapped |
| `in_game/common/death_reason/` | ui_data | unmapped |
| `in_game/common/designated_heir_reason/` | ui_data | unmapped |
| `main_menu/common/game_concepts/` | game_concepts | unmapped |
| `main_menu/common/named_colors/` | ui_data | unmapped |
| `main_menu/common/coat_of_arms/` | ui_data | unmapped |
| `main_menu/common/flag_definitions/` | ui_data | unmapped |

---

## Annotation Index

System metadata (stage, cluster, version) is maintained in [`_system_index.json`](_system_index.json).
System relationships are maintained in [`_system_edges.json`](_system_edges.json).

## System Relationships

The annotation project tracks cross-system relationships as a typed edge graph for future interactive visualization.

**Data files:**
- `_system_index.json` — node registry: system id, label, annotation path, stage, cluster, verified game version, summary
- `_system_edges.json` — edge list: source → target with typed relationships

**Edge types:**
| Type | Meaning |
|---|---|
| `registers` | System A lists IDs defined in system B |
| `references` | System A uses IDs from system B |
| `shared_mechanic` | Systems use the same field pattern (e.g. opinions blocks) |
| `modifies` | System A pushes values into system B (e.g. monthly_towards_*) |
| `hierarchy` | System A contains system B |

## TODO

- [ ] **Mermaid diagram** — generate static flowchart from `_system_index.json` + `_system_edges.json` once annotation pass is substantially complete
- [ ] **Interactive graph viewer** — D3/Cytoscape/vis.js consuming both JSON files; features: click node → annotation, filter by edge type, cluster zoom, version-stale coloring
- [ ] **Remaining tiers** — Tier 6 (Scripted infrastructure), Tier 7 (AI), Tier 8 (UI/Presentation/Niche) still need annotation
