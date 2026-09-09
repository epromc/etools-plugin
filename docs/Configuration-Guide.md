---
description: Complete reference for configuring eTools settings, messages, and custom tool archetypes.
---

# ⚙️ Configuration Guide

All aspects of **eTools** can be easily customized across three primary configuration files located in `/plugins/eTools/`:

{% hint style="tip" %}
All configuration changes can be reloaded on-the-fly without restarting your server by running `/etools reload`.
{% endhint %}

---

## 1. `config.yml` (Server-Wide Settings)

Controls core performance thresholds, scheduler frequencies, database connections, and audio-visual cues:

```yaml
settings:
  # How often (in seconds) the timer task checks online players' active items
  timer-interval-seconds: 1

  # Enable instant expiration checks when players open containers (Chests, Barrels, Shulkers, etc.)
  container-validation: true

  # Merge nearby drop items to prevent entity lag when breaking large areas
  batch-drops: true

  # Max log blocks an axe can fell in a single swing (prevents freezing on massive trees)
  max-tree-feller-blocks: 500

  # Lifespan warning thresholds (in seconds) that trigger sound and action bar alerts
  # 300 = 5 minutes, 60 = 1 minute
  alert-thresholds:
    - 300
    - 60

# Region & Claim Protection Integrations
hooks:
  worldguard: true
  griefprevention: true

# Database Configuration (SQLite for local file, MySQL/MariaDB for remote network)
database:
  type: SQLITE # Options: SQLITE or MYSQL
  sqlite:
    file: "database.db"

# Sound effects for lifespan alerts & destruction
sounds:
  alert:
    name: "BLOCK_NOTE_BLOCK_PLING"
    volume: 1.0
    pitch: 1.8
  expired:
    name: "BLOCK_AMETHYST_CLUSTER_BREAK"
    volume: 1.2
    pitch: 0.9
```

---

## 2. `messages.yml` (Localization & Styling)

Every message, prefix, alert, and notification can be tailored to match your server's theme.

{% hint style="info" %}
**Formatting Engines:** Full support for modern **Adventure MiniMessage** tags (e.g. `<gradient:#HEX1:#HEX2>`, `<#HEX>`, `<hover>`, `<click>`) and legacy color codes (`&a`, `&b`, etc.).
{% endhint %}

```yaml
prefix: "<gradient:#B983FF:#7F00FF><b>ᴇᴛᴏᴏʟs</b></gradient> <dark_gray>»</dark_gray> "

messages:
  no-permission: "<red>ʏᴏᴜ ᴅᴏ ɴᴏᴛ ʜᴀᴠᴇ ᴘᴇʀᴍɪssɪᴏɴ ᴛᴏ ᴇxᴇᴄᴜᴛᴇ ᴛʜɪs ᴄᴏᴍᴍᴀɴᴅ.</red>"
  player-not-found: "<red>ᴘʟᴀʏᴇʀ <gold>{player}</gold> ᴡᴀs ɴᴏᴛ ꜰᴏᴜɴᴅ ᴏɴʟɪɴᴇ.</red>"
  tool-given: "<gray>ɢᴀᴠᴇ <yellow>{amount}x</yellow> {tool} <gray>ᴛᴏ</gray> <gold>{player}</gold> <gray>(ʟɪꜰᴇsᴘᴀɴ: <#B983FF>{duration}</#B983FF>).</gray>"
  tool-received: "<gray>ʏᴏᴜ ʀᴇᴄᴇɪᴠᴇᴅ {tool} <gray>(ʟɪꜰᴇsᴘᴀɴ: <#B983FF>{duration}</#B983FF>).</gray>"
  # ... (all in-game messages are fully customizable)
```

---

## 3. `tools.yml` (Custom Tool Creation)

You have total freedom over custom tools. You are never limited to default templates—create any custom tool archetype with unique models, sounds, particles, and enchantments.

### Configuration Specification:

```yaml
tools:
  your_tool_id:
    # Tool archetype: DRILL, SHOVEL, AXE, HOE, SHEARS, INFINITE_PEARL, INFINITE_ROCKET,
    # INFINITE_WATER, INFINITE_LAVA, INFINITE_GOLDEN_APPLE, INFINITE_STEAK
    type: DRILL

    # Base Minecraft item material
    base-item: NETHERITE_PICKAXE

    # Custom Model Data for custom resource pack models / textures (optional)
    custom-model-data: 10001

    # Display name with MiniMessage gradient support
    display-name: "<gradient:#B983FF:#7F00FF><b>ᴀᴍᴇᴛʜʏsᴛ ᴅʀɪʟʟ</b></gradient>"

    # Custom lore lines (<time_remaining> placeholder automatically updates)
    lore:
      - "<dark_gray>─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─</dark_gray>"
      - "<gray>ᴍɪɴᴇs ᴀ <#B983FF>3x3</#B983FF> ᴀʀᴇᴀ ɪɴsᴛᴀɴᴛʟʏ ɪɴ ᴛʜᴇ"
      - "<gray>ᴅɪʀᴇᴄᴛɪᴏɴ ʏᴏᴜ ᴀʀᴇ ʟᴏᴏᴋɪɴɢ."
      - ""
      - "<dark_gray>▸</dark_gray> <gray>ᴛʏᴘᴇ:</gray> <#B983FF>ᴅɪʀᴇᴄᴛɪᴏɴᴀʟ ᴅʀɪʟʟ</#B983FF>"
      - "<dark_gray>▸</dark_gray> <gray>ʀᴀᴅɪᴜs:</gray> <#B983FF>3x3 ʙʟᴏᴄᴋs</#B983FF>"
      - "<dark_gray>▸</dark_gray> <gray>ʟɪꜰᴇsᴘᴀɴ:</gray> <#B983FF><time_remaining></#B983FF>"
      - "<dark_gray>─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─</dark_gray>"

    # Mining / tilling radius (3 = 3x3, 5 = 5x5)
    radius: 3

    # Lifespan rules
    lifespan:
      mode: "ONLINE_TIME" # ONLINE_TIME, REAL_TIME, or UNLIMITED
      default-duration: "4h" # Default granted lifespan (e.g., 30m, 1h, 4h, 7d, permanent)

    # Item flags & safeguards
    unbreakable: true # Prevents vanilla durability depletion
    keep-on-death: true # Retained in inventory upon player death
    prevent-anvil: true # Disallows renaming or repair exploits in anvils
    prevent-grindstone: true # Disallows stripping enchantments or XP farming
    glow: true # Displays enchantment shimmer

    # Aesthetic visual particle effects
    particle:
      enabled: true
      type: "DUST"
      color: "#B983FF"
      size: 1.0
      count: 12
      speed: 0.05

    # Aesthetic sound feedback on use
    sound:
      enabled: true
      name: "BLOCK_AMETHYST_BLOCK_CHIME"
      volume: 1.0
      pitch: 1.5

    # Custom enchantments and flags
    enchantments:
      - "EFFICIENCY:6"
      - "FORTUNE:3"
    hide-enchantments: true
    hide-attributes: true
```
