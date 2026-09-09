---
description: Complete reference for all eTools player and administrative commands and permissions.
---

# ⌨️ Commands & Permissions

## 📌 Commands Reference

### 1. `/etools settings`
* **Permission:** `etools.settings` (Default: All players)
* **Description:** Opens the personal player settings GUI to configure individual gameplay preferences:
  * Visual particle effects (Enabled / Disabled).
  * Audio sound effects (Enabled / Disabled).
  * **Natural Blocks Only** mode (Restricts custom tools to 1x1 on player-placed blocks to protect houses and buildings).

---

### 2. `/etools give <player> <tool_id> [duration] [amount]`
* **Permission:** `etools.admin` (Default: OP)
* **Description:** Grants a custom tool to a specified player with an optional custom lifespan.
* **Duration Format:**
  * `30m` = 30 Minutes
  * `1h` = 1 Hour
  * `4h` = 4 Hours
  * `7d` = 7 Days
  * `permanent` = Never expires (Unlimited)
* **Examples:**
  * `/etools give Steve amethyst_drill 4h`
  * `/etools give Alex emerald_hoe permanent 1`
  * `/etools give Steve infinite_pearl`

---

### 3. `/etools duration <set|add|remove> <duration>`
* **Permission:** `etools.admin` (Default: OP)
* **Description:** Modifies the remaining lifespan of the custom tool currently held in the player's main hand.
* **Sub-commands:**
  * `set <duration>`: Resets the lifespan to a specific time (e.g., `/etools duration set 2h` or `/etools duration set permanent`).
  * `add <duration>`: Adds time to the tool's lifespan (e.g., `/etools duration add 30m`).
  * `remove <duration>`: Deducts time from the tool's lifespan (e.g., `/etools duration remove 1h`).

---

### 4. `/etools recall [player|all]` & `/etools recall confirm`
* **Permission:** `etools.admin` (Default: OP)
* **Description:** Emergency confiscation system that permanently purges all eTools items across the server (Two-Stage Confirmation).

{% hint style="danger" %}
**Caution:** `/etools recall confirm` is an irreversible action. It sweeps inventories, open chests, ground items, containers across loaded chunks, and marks unloaded chunk items for deletion.
{% endhint %}

* **Usage Flow:**
  1. Execute `/etools recall all` (or `/etools recall Steve`).
  2. The plugin will prompt an alert in chat:
     `» ᴡᴀʀɴɪɴɢ: ᴛʜɪs ᴡɪʟʟ ʀᴇᴄᴀʟʟ ᴀʟʟ ᴇᴛᴏᴏʟs ɪᴛᴇᴍs ꜰʀᴏᴍ ALL ONLINE PLAYERS! ᴛʏᴘᴇ /etools recall confirm ᴡɪᴛʜɪɴ 15s ᴛᴏ ᴘʀᴏᴄᴇᴇᴅ.`
  3. Type `/etools recall confirm` within 15 seconds.
  4. All player inventories, armor, open containers, world blocks (Chests, Hoppers, Barrels, Shulkers), entities (Minecarts, Donkeys), and ground drop items are cleaned instantly.

---

### 5. `/etools list`
* **Permission:** `etools.admin` (Default: OP)
* **Description:** Displays an aesthetic list of all registered custom tools, their category, and their default expiry mode in chat.

---

### 6. `/etools reload`
* **Permission:** `etools.admin` (Default: OP)
* **Description:** Reloads `config.yml`, `messages.yml`, and `tools.yml` without requiring a server restart.

---

### 7. `/etools help`
* **Permission:** `etools.admin` (Default: OP)
* **Description:** Displays an interactive command guide with clickable command suggestions.

---

## 🔑 Permissions Reference

| Permission Node | Default | Description |
| :--- | :---: | :--- |
| `etools.admin` | `op` | Grants access to all administrative commands. |
| `etools.settings` | `true` | Allows players to open the `/etools settings` GUI. |
| `etools.use.*` | `true` | Allows players to use all custom tools and infinite utilities. |
| `etools.use.<tool_id>` | `true` | Allows players to use a specific tool (e.g., `etools.use.amethyst_drill`). |
| `etools.bypass.cooldown` | `false` | Bypasses cooldown restrictions on infinite utility items. |
| `etools.bypass.timer` | `false` | Prevents custom tools from expiring or counting down their active time. |
