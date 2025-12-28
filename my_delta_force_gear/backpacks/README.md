# Backpacks

This folder contains all DayZ backpack JSON data for  
[My Delta Force Gear](https://steamcommunity.com/sharedfiles/filedetails/?id=3427626164)

Each JSON file represents a single backpack, manually converted from the mod’s CPP configuration files.

This repository does NOT contain the mod itself.  
It only provides structured, publicly derived information in JSON format.

---

## Schema Versions

All backpack JSON files include a `_schema` field that defines the structure and supported features.

Bots, scripts, and tools MUST check `_schema` before processing data.

### Schema Overview

| Schema | Description |
|------|------------|
| v1 | Standard backpacks |
| v2 | Backpacks with armor values |
| v3 | Backpacks with attachment damage transfer |

### Schema Details

### v1 – Standard Backpack
Base schema used for normal backpacks.

Includes:
- Inventory size
- Attachments
- Environmental values
- Repair data

Does NOT include:
- Armor values
- Attachment damage transfer

---

### v2 – Armored Backpack
Extends v1 by adding armor data extracted from GlobalArmor in CPP.

Adds:
- armor field

Used for:
- Bulletproof shields
- Armored backpacks

---

### v3 – Attachment Damage Transfer
Extends v1 (and may also include v2 features).

Adds:
- transferToAttachmentsCoef

Used when:
- Damage taken by the backpack is partially transferred to attached items

---

## JSON Fields

### Core Fields (All Schemas)

| Field | Description |
|-----|------------|
| `_schema` | Schema version (`v1`, `v2`, `v3`) |
| `name` | Array: `[spawnName, displayName]` |
| `description` | Item description |
| `rarity` | Item rarity (`-1` = not set by mod) |
| `class` | Loot tier (`-1` = not set by mod, 1–5 = Tier 1–5) |
| `weight` | Weight in grams |
| `itemSize` | Inventory size (example: "3x3") |
| `img` | `N/A` if not set, otherwise relative path |
| `hitpoints` | Item durability |
| `slots.Total` | Total cargo slots |
| `slots.H` | Horizontal grid size |
| `slots.V` | Vertical grid size |
| `attachments` | Supported attachments and their slot counts |
| `repairs` | Repair items and effectiveness percentage |
| `player_hooks` | Player attachment slots (e.g. `Back`, `Armband`) |

---

## Environmental Properties

| Field | Description |
|------|------------|
| `absorbency` | Water absorption percentage |
| `varWetMax` | Maximum wetness level |
| `heatIsolation` | Heat insulation capability |

All values use a 0 – 1 range.

If a value is not defined by the mod, it may be set to `null`.

---

## Armor Data (v2 only)

```json
"armor": {
    "Projectile": { "Health": 0.2, "Blood": 0, "Shock": 0.2 },
    "Melee": { "Health": 0.2, "Blood": 0, "Shock": 0.2 },
    "Infected": { "Health": 0.2, "Blood": 0, "Shock": 0.2 },
    "FragGrenade": { "Health": 0.2, "Blood": 0, "Shock": 0.2 }
}
```

Each damage class defines reduction values for:
- Health
- Blood
- Shock

Lower values indicate stronger protection.

---

## Attachment Damage Transfer (v3 only)

| Field | Description |
|------|------------|
| `transferToAttachmentsCoef` | Damage coefficient applied to attachments when the backpack takes damage |

Examples:
- `0.5` → 50% of damage transfers to attachments
- `null` → not defined or not used

---

## Attachments

The attachments object defines which items can be attached and how many slots are available.

| Attachment Type | Description |
|-----------------|-------------|
| Rifle | Rifle attachment slots |
| Pouches | Pouch slots |
| Glowstick | Glowstick slots |
| Strap | Strap slots |
| Canteen | Canteen slots |
| Rope | Rope slots |
| Hatchet | Hatchet slots |
| Sleeping Bag | Sleeping bag slots |
| Gloves | Glove attachment slots |
| Baseball Bat | Baseball bat attachment slots |

Example:
```json
"Rifle": 2
```

Means the backpack supports two rifle attachments.

---

## Usage

- Intended primarily for bots and automation tools
- Can be used by players and developers as a reference
- Always validate `_schema` before parsing

---

## Thanks

Special thanks to [MY] (https://discord.com/users/1279413978132647989) for taking the time to answer questions and provide clarification via Discord on how certain systems and values work within the mod.

---

## Notes

- File names use CamelCase with underscores
- Minor inaccuracies may exist due to manual CPP conversion
- All data is sourced from publicly available mod files
- This repository does not claim ownership of the mod
