# Goods
**Stage:** complete
**Keywords:** goods, good, price, prices, goods_demand, goods_demand_category, demand_add, demand_multiply, default_market_price, transport_cost, base_production, category, method, food, is_slaves, inflation, pop_demand, regiment_construction, regiment_maintenance, building_construction, building_maintenance

> **System type: Data/Reference**

## Overview
Goods are the tradeable commodities that flow through EU5's market system. Each good definition sets its base market price, extraction method, food value, transport cost, and per-pop-type demand modifiers. Three companion systems extend this: `prices/` defines named cost bundles (gold, manpower, resources) referenced by actions and buildings; `goods_demand/` defines named demand bundles that attach recurring consumption to armies, buildings, and pops; and `goods_demand_category/` defines the display categories those bundles belong to. Together these four folders form the complete goods economy layer. Modders add new goods to introduce new trade commodities, adjust economic balance, or attach new resources to buildings and units.

## Vanilla File Locations
- `in_game/common/goods/` — goods definitions split by type (5 files + readme)
  - `00_raw_materials.txt` — mined/gathered/farmed inputs (horses, clay, coal, etc.)
  - `01_plantation_goods.txt` — colonial plantation goods (sugar, tobacco, spices, etc.)
  - `02_produced_goods.txt` — manufactured goods (firearms, cloth, porcelain, etc.)
  - `03_food.txt` — food goods (wheat, fish, salt, etc.)
  - `04_special.txt` — slaves_goods
- `in_game/common/prices/` — named price definitions (6 files + readme)
- `in_game/common/goods_demand/` — named demand bundles (7 files)
- `in_game/common/goods_demand_category/00_default.txt` — demand display categories
- Full file list in `_file_index.csv`.

## Block Structure

### Good Definition
```pdx
<good_id> = {
    # --- Classification ---
    category = raw_material/produced    # defaults raw_material
    method   = mining/farming/hunting/gathering/forestry   # defaults farming

    # --- Economy ---
    default_market_price = <float>      # base price on a market (default 1)
    transport_cost       = <float>      # how expensive to ship (default 1)
    base_production      = <float>      # base amount produced per RGO slot (default 0)

    # --- Food ---
    food = <float>                      # food value provided when consumed (default 0)

    # --- Flags ---
    is_slaves          = yes/no         # marks this as a slave good (default no)
    block_rgo_upgrade  = yes/no         # prevents RGO expansion for this good (default no)
    inflation          = yes/no         # production causes inflation (default no)
    origin_in_old_world = yes/no        # used for colonial restriction logic

    # --- Display ---
    color = <color_key>
    ai_rgo_size_importance       = <float>  # AI penalty for building cities on this RGO
    ai_rgo_expansion_priority    = <float>  # AI preference for expanding this RGO

    # --- Per-pop demand modifiers ---
    demand_add = {
        all            = <float>    # adds flat demand for all pop types
        <pop_type_id>  = <float>    # adds flat demand for a specific pop type
    }
    demand_multiply = {
        upper          = <float>    # multiplies demand for upper-class pops
        <pop_type_id>  = <float>    # multiplies demand for a specific pop type
    }

    # --- Wealth thresholds ---
    development_threshold = <int>       # minimum development before this good appears
    wealth_impact_threshold = {
        all = <float>                   # wealth level at which pop demand starts scaling
    }

    # --- Tagging ---
    custom_tags = { <strings> }         # tested via good_has_custom_tag trigger
}
```

### Price Definition
```pdx
<price_id> = {
    # Resource costs (flat amounts; negative = reward)
    gold                = <float>
    manpower            = <float>
    sailors             = <float>
    stability           = <float>
    war_exhaustion      = <float>
    inflation           = <float>
    prestige            = <float>
    army_tradition      = <float>
    navy_tradition      = <float>
    government_power    = <float>

    # Religion-specific resources
    karma / religious_influence / purity / honor / doom / rite_power /
    yanantin / complacency / righteousness / harmony / self_control = <float>

    # Scaled variants (multiply against country's own value)
    scaled_gold         = <float>       # gold cost = country_base × scaled_gold
    scaled_manpower     = <float>
    scaled_sailors      = <float>
    scaled_recipient_gold = <float>     # paid by the recipient instead
    gold_per_pop        = <float>       # cost scales per pop count

    # Bounds
    min       = <float>     # minimum total after modifiers
    min_scale = <float>     # minimum before modifiers
    max_scale = <float>     # maximum before modifiers
}
```

### Goods Demand Bundle
```pdx
<demand_id> = {
    <good_id> = <float>     # amount of this good consumed per unit/building/pop per month
    category  = <demand_category_id>    # which display group this belongs to
}
```

### Goods Demand Category
```pdx
<category_id> = {
    display = integer/pop   # how quantities are displayed in the UI
}
```

## Key Fields Reference
| Field | Purpose | Key constraint |
|---|---|---|
| `category` | Classifies as raw material or processed good | Affects market behaviour and UI grouping; `produced` goods typically require manufacturing buildings |
| `method` | Extraction type for RGO | Determines which RGO building types can produce this good |
| `default_market_price` | Base price before supply/demand adjustments | Higher prices increase tax revenue and trade value |
| `transport_cost` | Multiplier on shipping cost | High values (2.0) make a good expensive to trade across distance |
| `base_production` | Default RGO output without buildings | Most goods have 0 and rely entirely on buildings |
| `food` | Food units provided per unit consumed | Only food-category goods should have non-zero values |
| `demand_add` | Flat demand added per pop type per month | `all` applies to every pop type; specific pop types override `all` additively |
| `demand_multiply` | Multiplier on demand for a pop category | `upper` applies to all upper-class pops; individual pop types also valid |
| `is_slaves` | Tags the good as a slave commodity | Only one vanilla good uses this; affects special demand mechanics |
| `inflation = yes` | Production of this good generates inflation | Only applies to goods that represent money-substitutes (precious metals) |
| `scaled_gold` in price | Cost scales as a fraction of a country stat | `scaled_gold = 5.0` = 5× the country's base gold value |
| `demand_id category` | Assigns the bundle to a display group | Must match an ID in `goods_demand_category/` |

## Modding Notes
- **Adding a new good** requires entries in `goods/`, then referencing the good ID wherever it should be consumed (demand bundles, building inputs in production methods, good-specific triggers). The market system picks it up automatically from the goods folder.
- **`demand_add` and `demand_multiply`** work together per pop type. Demand = (base + `demand_add`) × `demand_multiply`. The `all` key is a shorthand for all pop types simultaneously; specific pop type keys add on top of or override `all` for that type.
- **`wealth_impact_threshold`** sets the wealth level above which pops start consuming this good. Below the threshold, demand is effectively zero for those pops. Used to gate luxury goods (porcelain, jewelry) behind wealth requirements.
- **Price definitions** (`prices/`) are referenced by actions, buildings, and other systems using `price:<price_id>`. They are not goods — they are named resource cost bundles. `scaled_gold` makes costs proportional to a country's economy, while flat `gold` is always the same amount.
- **Goods demand bundles** (`goods_demand/`) are named lists of `<good_id> = <float>` pairs that the engine draws from automatically for armies, buildings, and pops. A bundle named `infantry_construction` is consumed when building infantry. The `category` field determines how it is grouped in the demand UI.
- **`goods_demand_category/`** only defines display categories, not mechanics. Adding new categories requires corresponding UI entries to appear correctly.
- **`inflation = yes`** on a good (e.g. gold ore) means that high production of that good inflates the economy. Do not set this on ordinary goods.
- **`block_rgo_upgrade = yes`** prevents the RGO for this good from being expanded via scripted building. Useful for goods that should remain fixed-output (e.g. slaves, special resources).
- **Cross-system:** good IDs are referenced in production methods (`buildings.md`), demand bundles, pop type demand scripts, and market triggers. Renaming a good breaks all these references silently.

## Example

**Good definition** — `horses` (raw material, high transport cost, noble demand):
```pdx
horses = {
    method   = farming
    category = raw_material
    color    = goods_horses
    default_market_price = 3
    transport_cost       = 2     # expensive to move — regional price variation common
    demand_add = {
        nobles = 0.25            # only nobles have baseline demand
    }
    origin_in_old_world = yes
    custom_tags = { old_world_goods }
}
```

**Price definition** — `embrace_institution` (scaled gold + stability cost):
```pdx
embrace_institution = {
    scaled_gold = 5.0    # cost = 5× country's base gold modifier
    stability   = 50     # also costs stability points
}
```

**Demand bundle** — `cavalry_construction` (goods consumed when recruiting cavalry):
```pdx
cavalry_construction = {
    leather  = 0.1
    cloth    = 0.1
    horses   = 0.5
    weaponry = 0.1
    category = regiment_construction
}
```
