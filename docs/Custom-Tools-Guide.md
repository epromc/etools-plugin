---
description: Comprehensive breakdown of all custom tool archetypes, mechanics, and capabilities in eTools.
---

# 🌾 Custom Tools & Utilities

**eTools** supports an extensive lineup of custom tool archetypes powered by cutting-edge mechanics:

---

## ⛏️ 1. Directional Drills & Shovels (`DRILL`, `SHOVEL`)

* **Mechanics:** Mines or digs in a **3x3** (or **5x5**) area based on the player's line of sight:
  * Facing Up / Down: Clears horizontal planes (X and Z axis).
  * Facing North / South: Clears vertical planes (X and Y axis).
  * Facing East / West: Clears vertical planes (Z and Y axis).
* **Drill Target Blocks:** Stone, Deepslate, Netherrack, End Stone, Granite, Diorite, Andesite, Tuff, Basalt, Blackstone, Sandstone, and all mining ores.
* **Shovel Target Blocks:** Dirt, Grass Blocks, Sand, Gravel, Clay, Mud, Soul Sand, Soul Soil, and Snow.
* **Native Item Merging:** Mined items drop naturally and merge automatically to minimize entity count and preserve server performance.

{% hint style="tip" %}
**Directional Intelligence:** Mining floors while looking straight down will clear a flat 3x3 beneath your feet. Mining walls will open a 3x3 tunnel entrance facing you!
{% endhint %}

---

## 🪓 2. Tree Feller Axe (`AXE`)

* **Mechanics:** Utilizes a **Breadth-First Search (BFS)** queue algorithm to fell an entire connected tree up to `max-tree-feller-blocks` (default: 500 blocks) in one swing.
* **Leaf Auto-Decay:** Connected leaves decay in cascading order so trees never leave awkward floating foliage.
* **Protection Integration:** Validates region permissions per block to ensure the feller does not cross into another player's protected land claim.

---

## 🌾 3. Agricultural Hoes (`HOE`) - Harvester & Tiller

Hoes in eTools combine three essential farming functions:

### A. AoE Soil Tilling (Right-Click)
* **Right-Click** on tillable soil (`GRASS_BLOCK`, `DIRT`, `DIRT_PATH`, `COARSE_DIRT`, `ROOTED_DIRT`) converts the entire area into **Farmland**.
  * `amethyst_hoe`: **3x3** area (up to 9 blocks).
  * `emerald_hoe`: **5x5** area (up to 25 blocks).
* **Adaptive Elevation (`dy: -1 to +1`):** Seamlessly tills undulating terrain, hills, and stepped terraces.
* **Grass Clearing:** Short grass, tall grass, and ferns sitting on top are cleared automatically.
* **Rooted Dirt Mechanic:** Tilling rooted dirt naturally drops `HANGING_ROOTS` items, matching vanilla behavior.

### B. AoE Harvesting & Auto-Replanting (Left or Right-Click)
* **Right-Click or Left-Click** on mature crops (Wheat, Carrots, Potatoes, Beetroots, Nether Wart, Cocoa, Pitcher Crops, Torchflowers) harvests all mature crops within the 3x3 or 5x5 radius.
* Crop yields drop naturally at the crop's location, and seeds are replanted at age 0 with anti-desync protection.
* Clicking the farmland block underneath a crop will automatically redirect the harvest to the crop above.

### C. Hoe-Mineable AoE Blocks (3x3 & 5x5)
* Supports directional 3x3 and 5x5 mining for blocks where the hoe is the optimal tool:
  * Hay Bales (`HAY_BLOCK`), Targets, Dried Kelp Blocks, Shroomlights, Sponges, Wet Sponges.
  * All Sculk family blocks (`SCULK`, `SCULK_CATALYST`, `SCULK_SHRIEKER`, `SCULK_SENSOR`, `SCULK_VEIN`).
  * All tree leaves (`Tag.LEAVES`), Moss Blocks, and Moss Carpets.
  * Nether Wart Blocks, Warped Wart Blocks, Melons, Pumpkins, and Froglights.

---

## ✂️ 4. AoE Shears (`SHEARS`)

* **Mass Sheep Shearing:** Right-clicking an adult sheep shears all adult sheep in a 5x5 radius simultaneously, dropping wool matching each sheep's natural color.
* **Foliage Pruning:** Rapidly harvests leaves, cobwebs, vines, and tall grass in a 3x3 radius.

---

## ♾️ 5. Infinite Utility Items

* **Infinite Ender Pearl (`infinite_pearl`):**
  * Launches ender pearls without consuming the item from the player's hand.
  * Features a configurable cooldown with live countdown alerts on the Action Bar.
* **Infinite Firework Rocket (`infinite_rocket`):**
  * Provides Elytra flight boosts without depleting fireworks.
* **Infinite Buckets (`infinite_water` & `infinite_lava`):**
  * Places infinite water or lava sources.
  * **Anti-Abuse Auto-Dissolve:** Placed liquids automatically evaporate after 10 seconds to prevent griefing, trolling, or world flooding.
  * **Anti-Infinite Source:** Temporary water cannot form infinite water pools and cannot be collected back into regular vanilla buckets.
* **Infinite Food (`infinite_golden_apple` & `infinite_steak`):**
  * Food is never consumed from hand.
  * Restores hunger, saturation, and applies potion buffs (Regeneration II & Absorption I for Golden Apples) with fair cooldown controls.

---

## 🛡️ "Natural Blocks Only" Mode

Every player can open `/etools settings`:
* When **Natural Blocks Only** is enabled:
  * If a player strikes a block that was previously placed by a player, the tool is restricted to **1 single block** (1x1).
  * When mining natural underground caves or operating a Cobblestone Generator, the tool continues to mine at full **3x3** or **5x5**.
  * Prevents catastrophic accidents where players accidentally destroy their bases, walls, or chest rooms.

{% hint style="info" %}
**Persistent Tracking:** Player-placed blocks are recorded in chunk persistent data containers (PDC) and synchronized with CoreProtect (if installed), making block data persistent across server restarts.
{% endhint %}
