---
description: Step-by-step instructions for installing and setting up eTools on Paper, Purpur, or Folia.
---

# 📥 Installation & Setup

## 📌 System Requirements

* **Java Version:** Java 21 or higher.
* **Server Software:**
  * **Paper** 1.21.x (Recommended)
  * **Purpur** 1.21.x
  * **Folia** 1.21.x (Native support with Region & Entity Schedulers)
  * **Spigot** 1.21.x

{% hint style="info" %}
**Folia Compatibility:** eTools automatically detects Folia and hooks into regionized multithreading. No manual flags or configurations are required!
{% endhint %}

---

## 📥 Installation Steps

1. **Download the Plugin:**
   Download `eTools-0.0.1-RELEASE.jar` from your official release source or Modrinth.
2. **Place in Server:**
   Copy the JAR file into your server's `/plugins/` directory.
3. **Start the Server:**
   Launch your server (`java -jar paper.jar`). The plugin will automatically:
   * Download runtime dependencies (`HikariCP` and `sqlite-jdbc`) to your server's `libraries/` directory.
   * Generate default configuration files in `/plugins/eTools/`:
     * `config.yml`
     * `messages.yml`
     * `tools.yml`
     * `database.db` (when using SQLite mode)
4. **Verification:**
   Check your server console. You will be greeted by the eTools startup banner:
   ```text
    ______     ______   ______     ______     __         ______    
   /\  ___\   /\__  _\ /\  __ \   /\  __ \   /\ \       /\  ___\   
   \ \  __\   \/_/\ \/ \ \ \/\ \  \ \ \/\ \  \ \ \____  \ \___  \  
    \ \_____\    \ \_\  \ \_____\  \ \_____\  \ \_____\  \/\_____\ 
     \/_____/     \/_/   \/_____/   \/_____/   \/_____/   \/_____/ 
      by epromite & epromc • v0.0.1-RELEASE
   ```

---

## 🗄️ Database Setup (SQLite vs. MySQL)

Open `/plugins/eTools/config.yml`:

### Option 1: SQLite (Default - Recommended for Single Servers)
Requires zero external setup. All data is saved locally to `database.db`.
```yaml
database:
  type: SQLITE
  sqlite:
    file: "database.db"
```

### Option 2: MySQL / MariaDB (Recommended for Networks / Proxies)
If you operate a multi-server network (BungeeCord / Velocity) and wish to synchronize tool ownership and usage across instances:
```yaml
database:
  type: MYSQL
  mysql:
    host: "localhost"
    port: 3306
    database: "etools"
    username: "your_username"
    password: "your_password"
    ssl: false
  pool:
    maximum-pool-size: 10
    minimum-idle: 5
    maximum-lifetime: 1800000
    connection-timeout: 5000
```

---

## 🔌 Optional Integrations (Hooks)

eTools automatically detects and hooks into the following plugins:

* **WorldGuard (v7.0+):**
  Prevents area tools (3x3 / 5x5) from breaking blocks inside protected regions without break permissions (`canBreak` flag).
* **GriefPrevention:**
  Respects player land claims. Unauthorized players cannot mine, dig, or till within another player's claim.
* **CoreProtect:**
  Examines historical player block-placement logs to enhance the **Natural Blocks Only** protection mode (`/etools settings`).

{% hint style="success" %}
All hooks are soft-dependencies. If these plugins are not installed, eTools will run standalone without any issues.
{% endhint %}
