# EnvyEssentialsPremium

A comprehensive and premium utility plugin for Unturned, designed to enhance server management, gameplay experience, and administrative control.

---

## 📑 Table of Contents
1. [Requirements](#-requirements)
2. [Privacy and Tracking](#-privacy-and-tracking)
3. [Global Configuration](#-global-configuration)
4. [Kits System](#kits-system)
5. [Teleportation (TPA) System](#teleportation-tpa-system)
6. [Home & Warp Systems](#home--warp-systems)
7. [Stats & Rankings](#stats--rankings)
8. [Rank Advancement System](#rank-advancement-system)
9. [Vaults Virtual Storage](#vaults-virtual-storage)
10. [Filter System (Auto-Pickup)](#filter-system-auto-pickup)
11. [Catch Inventory System](#catch-inventory-system)
12. [Utility Modules](#utility-modules)
13. [Administrative Commands](#administrative-commands)
14. [Complete Command Reference](#complete-command-reference)

---

## ⚠️ Requirements

> [!IMPORTANT]
> This plugin **requires OpenMod** to function. Installation is mandatory. The plugin is designed to attempt an automatic installation of OpenMod if it is not detected on startup.

---

## 🔒 Privacy and Tracking

This plugin monitors player connectivity data to ensure server security and identify potential alt-account abuse.
- **Data Collected:** Hardware ID (HWID) and Username.
- **Storage:** Data is logged in the `PlayersData.json` file inside the `EssentialsX/Data` folder.
- **Commands:** The `/ess investigate [player]` command uses this data to track multi-accounts and historical connections.

---

## ⚙️ Global Configuration

### DropEssentialsXBanList
Enable or disable the private "creator-provided" ban list. This list contains known hackers and is maintained by the developers. While you cannot edit the list itself, you can choose whether or not to apply it to your server.

### EnableDAVEHealthBar (QoL)
Activates a visual health bar for bosses in the **Escalation** map mode. This improves the gameplay experience by allowing players to track boss damage in real-time.

### AutoPickupItems
Automatically collects items from the ground near the player. This is a configurable setting that can be toggled to streamline the looting process.

### ShowHealthBarOnHitPlayer
Enable or disable a visual health bar for players when you hit them. This feature allows you to see the current HP of an opponent immediately after dealing damage. It can be easily toggled on or off in the configuration file.

---

## Kits System

Kits allow players to receive predefined sets of items based on their rank or permissions.

#### Commands
1. `/createkit [name] [cooldown] [permission]` - Creates a kit using your current inventory contents.
2. `/deletekit [name]` - Deletes an existing kit.
3. `/kit [name]` - Claims a specific kit.
4. `/kits` - Displays all kits you have access to.
5. `/kitcooldown [kit] [seconds]` - Sets the cooldown for a specific kit.
6. `/kitvehicle [kit] [vehicleId]` - Attaches a vehicle to the kit.
7. `/migratekit` - **WARNING:** Attempts to migrate kits from "AviKits" to EssentialsX. This process may lose some items; review kits after migration.

#### Configuration Example
```xml
<?xml version="1.0" encoding="utf-8"?>
<EnvyKitsConfiguration>
  <UseEconomy>false</UseEconomy>
  <icon>URL_HERE</icon>
</EnvyKitsConfiguration>
```

#### Translations Snippet
```xml
<Translations>
  <Translation Id="kit:exist" Value="The kit already exists" />
  <Translation Id="kit:notfound" Value="The kit {0} does not exist" />
  <Translation Id="kit:cooldown" Value="You must wait {0} seconds to use this again" />
</Translations>
```

---

## Teleportation (TPA) System

A robust request-based teleportation system.

- **Usage:**
    - `/tpa [player]` - Send a teleport request.
    - `/tpa mode [global | group]` - Switch your TPA privacy mode.
        - `global`: Anyone can send you TPA requests.
        - `group`: Only members of your current group can request to teleport to you.

- **Configuration:**
    - **Interval:** Cooldown between teleports.
    - **Expiration:** Time before a request expires.

---

## Home & Warp Systems

### Home
Allows players to teleport to their claimed bed.
- **Command:** `/home`
- **Config:** `Block Moving` - If enabled, moving during the teleport countdown will cancel the action.

### Warps
Public or private points of interest.
- **Commands:** 
    - `/createwarp [name] [permission] [interval]` - Sets a warp at your current position.
    - `/warp [name]` - Teleport to the warp.
    - `/warps` - Lists all available warps.
- **Config:** `Interval` and `Expiration` times for warp usage.

---

## Stats & Rankings

Keep track of player accomplishments and performance on your server.
- **Commands:**
    - `/stats [player]` - View detailed Kills, Deaths, and other metrics.
    - `/ranking` - Displays the TOP players on the server.
- **Config:** `Top Max` - Set the number of players shown in the ranking.

---

## Rank Advancement System

Automatically promote players based on their in-game achievements.

#### Usage Guide
1. Enable `RankConfig` in the main configuration.
2. Run `/rocket reload EssentialsX`.
3. A `Ranks.json` file will be generated in the plugin folder.
4. Edit `Ranks.json` to define requirements (Zombies killed, Reputation, etc.).
5. Ranks are synced with `Permissions.xml` automatically.

#### Ranks.json Example
```json
{
  "Rank": [
    {
      "Name": "rank1",
      "Reputation": 1000,
      "Zombies": 500,
      "GroupToWin": "VIP"
    }
  ]
}
```

---

## Vaults Virtual Storage

Provides players with extra inventory space accessible via commands.

#### Commands
- `/vault [name]` - Opens the virtual storage.

#### Configuration
```xml
<Vaults>
  <Vault Name="VIP" Permission="vault.vip" SizeX="10" SizeY="10" />
  <Vault Name="USER" Permission="vault.user" SizeX="5" SizeY="5" />
</Vaults>
```

---

## Filter System (Auto-Pickup)

A specialized farming tool that automatically picks up specific items from defeated zombies.

- **How to use:**
    1. Use `/filter` to open the filter management UI.
    2. Add an item you wish to filter. **Note:** Adding an item consumes it (it is lost from your inventory to be "learned" by the filter).
    3. From now on, when you kill a zombie that drops that item, it will be automatically placed in your inventory.
- **Use Case:** Perfect for farm-heavy maps where picking up every item manually is tedious.

---

## Catch Inventory System

A powerful administration tool for live inventory inspection.

- **Usage:** `/catch [player]`
- **Capabilities:**
    - View the complete inventory of any online player like a storage box.
    - Manipulate items: Add, remove, or loot weapons and gear.
    - Manage clothing: Equip or remove hats, masks, vests, etc.

---

## Utility Modules

| Module | Description | Configuration Highlight |
| :--- | :--- | :--- |
| **Auto Clear** | Periodically deletes items, vehicles, or structures to reduce lag. | `Time_Items`, `Time_Vehicles`, `Time_Structures` |
| **Anti Spam** | Prevents chat flooding by enforcing a message interval. | `Interval` (Time between messages) |
| **NoName** | Hides player names for Roleplay purposes. | `Bypass` (Admins can still see names) |
| **Spawn Protection** | Grants invincibility or invisibility upon respawning. | `Protection Seconds`, `Vanish Mode` |
| **Death Messages** | Formatted alerts for player deaths. | `Show Location`, `Colors`, `Icons` |
| **Duty** | Allows admins to toggle their permissions on/off. | `/duty`, `Permission` |
| **Block Damage** | Restricts raid damage to structures/vehicles. | `BlockDamageOfBarricades`, `BlockDamageOfVehicles` |
| **CheckLag** | Automatically restarts the server if TPS drops too low. | `AutoShutdown`, `TPS Threshold` |
| **Block Repair** | Prevents players from repairing specific entities. | `Barricades`, `Structures`, `Vehicles` |
| **Decal Remover** | Clears blood/bullet decals to boost FPS. | `Enabled` |
| **CommandHelper** | Suggests valid commands (e.g., `/wa` -> `/warp`). | `Enabled`, `Custom Icon` |
| **Announcer** | Periodic automated server broadcasts. | `Interval`, `RandomMessages`, [Messages XML] |
| **TextCommands** | Create custom commands that return text (e.g., `/rules`). | [TextCommands XML] |
| **Anti Admin Abuse** | Alerts the public if an admin uses Vanish or God mode. | `ShowCommandsToThePublic` |
| **Old Gravity** | Reverts or modifies player gravity physics. | `GravityMultiplier` |
| **Join Messages** | Configurable join/leave notifications. | `ShowMessageOnJoin` |

---

## Administrative Commands

### Permanent Deletion (WB & WV)
> [!WARNING]
> These commands are destructive. Deleting an object or vehicle using these commands is **PERMANENT** and cannot be recovered.

- **WB (Work Block):** Deletes the **structure or barricade** you are currently looking at.
- **WV (Vehicle Block):** Deletes any **vehicle** you are looking at or nearby.

### Diagnostics & Management
- **Whois:** Identifies the owner of a structure, barricade, or vehicle.
- **WhatPerm:** Shows the permission node required for a specific command.
- **RepairV:** Repairs the vehicle you are looking at or currently sitting in.
- **ForceDrop [player]:** Forces a player to drop all inventory items onto the ground.
- **Storage:** View the contents of any chest or storage crate you are looking at.
- **TPS / UPS:** Displays server performance statistics.
- **Broma [player]:** For Fun/Troll - Spawns a massive amount of effects at the target's location.
- **Freeze / Unfreeze:** Restricts or restores a player's ability to move.
- **Boom [player]:** Creates a powerful explosion at a specific player's location.

---

## Complete Command Reference

| Command | Category | Description |
| :--- | :--- | :--- |
| `/ess` | Admin | Main menu: Investigate multis, reload modules, or list plugins. |
| `/hwid [player]` | Admin | Retrieves the unique Hardware ID of a player. |
| `/back` | Movement | Teleports you to your last known location. |
| `/speed [n]` | Movement | Increases or decreases your character speed. |
| `/sudo [p/*] [c]` | Admin | Force a player to execute a command. |
| `/door` | Admin | Remotely open or close any player-owned door. |
| `/storage` | Utility | View internal contents of chests and lockers. |
| `/filter` | Gameplay | Manage the zombie auto-pickup filter. |
| `/catch` | Admin | Advanced inventory inspection and management. |
| `/attach` | Gameplay | Customize weapon attachments. |
| `/mute / /unmute` | Admin | Manage player chat permissions. |
| `/whois` | Utility | Trace structure/vehicle ownership. |
| `/tps` | Diagnostic | View the server's Ticks Per Second. |
| `/ups` | Diagnostic | View the server's Updates Per Second status. |
| `/broma` | Fun | Spawn visual effect bursts on a player. |
| `/experience` | Admin | Manage player experience points. |
| `/reputation` | Admin | Manage player reputation level. |
| `/ascend` | Movement | Teleports the player to the next floor/level above. |
| `/descend` | Movement | Teleports the player to the next floor/level below. |
| `/boom [player]` | Fun | Detonates an explosion on a player. |
| `/clear <i/v> [r]` | Utility | Clear items (i) or vehicles (v) in a radius or all. |
| `/clearinventory` | Admin | Clears all items from a player's inventory. |
| `/getip [player]` | Admin | View a player's IP address. |
| `/i [id] [amount]` | Admin | Give a specific item to yourself. |
| `/jump` | Movement | Teleports the player to their aiming point. |
| `/maxskills` | Admin | Maximize all character skills instantly. |
| `/ping` | Utility | Check your current connection latency. |
| `/pos` | Utility | Display your current map coordinates. |
| `/pvp` | Gameplay | Toggle your PvP status. |
| `/suicide` | Gameplay | Commit character suicide. |
| `/tp [player]` | Movement | Teleport directly to another player. |
| `/tpall` | Admin | Teleport every online player to your location. |
| `/tell [p] [m]` | Utility | Send a private whisper to a player. |
| `/freeze / /unfreeze`| Admin | Prevent or allow player movement. |
| `/whatperm [cmd]` | Utility | Check required permission node for a command. |
| `/repair` | Utility | Repairs the item currently in hand. |
| `/repairv` | Utility | Repairs the vehicle being looked at or driven. |
| `/refuel` | Utility | Sets a vehicle's fuel to maximum. |
| `/unrefuel` | Utility | Empties a vehicle's fuel tank completely. |
| `/forcedrop [p]` | Admin | Forces a player to drop their entire inventory. |
| `/wb` | Admin | Permanently delete structures/barricades. |
| `/wv` | Admin | Permanently delete vehicles. |
