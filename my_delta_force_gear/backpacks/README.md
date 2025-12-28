# Backpacks

This folder contains all DayZ backpack JSON data for [My Delta Force Gear](https://steamcommunity.com/sharedfiles/filedetails/?id=3427626164).  
Each JSON file represents a single backpack, manually converted from mod CPP files.

## Schema Version

All JSON files include a `_schema` field to indicate the structure version:

- **`_schema: "v1"`** – current version
- Future updates may use `"v2"`, `"v3"`, etc.

Bots and scripts should use `_schema` to handle different formats safely.

## JSON Fields

| Field           | Description |
|-----------------|-------------|
| `_schema`       | Schema version (v1, v2, v3, etc.) |
| `Names`         | 1st name: in-game spawn/admin tool name; 2nd name: held/equipped display name |
| `Desc`          | Item description |
| `Rarity`        | Item rarity. `-1` = not set by mod. Others can set values for server setups (e.g., Common, Epic, Legendary, custom tables) |
| `Class`         | Loot tier. `-1` = not set by mod. Others can set: 1 = Tier 1 loot, …, 5 = Tier 5 loot |
| `Weight`        | Weight in grams |
| `Img`           | `N/A` if not set. If a path is provided, it’s relative to this JSON file |
| `Slots.Total`   | Total inventory slots |
| `Slots.H`       | Horizontal slots |
| `Slots.V`       | Vertical slots |
| `Attachments`   | What attachments it can take (see subcategory below). If empty, none are allowed |
| `Repairs`       | Items that can repair it and the effectiveness percentage |
| `Player Hooks`  | Which player slots it can attach to (e.g., back, armband) |

## Attachments Subcategory

The `Attachments` field supports the following types:

| Attachment Type | Notes |
|-----------------|------|
| Rifle           | Number of rifle slots |
| Pouches         | Number of pouch slots |
| Glowstick       | Number of glowstick slots |
| Strap           | Number of strap slots |
| Canteen         | Number of canteen slots |
| Rope            | Number of rope slots |
| Hatchet         | Number of hatchet slots |
| Sleeping Bag    | Number of sleeping bag slots |
| Gloves          | Number of glove attachments |
| Baseball Bat    | Number of baseball bat attachments |

> Example: `"Rifle": 2` means the backpack can hold **2 rifles**.

## Usage

- Bots and automation tools can read JSON files directly
- Players and developers can reference item stats
- Ensure `_schema` matches your parser logic

## Notes

- Files are named descriptively for easy automation
- Minor errors may exist due to manual conversion
- Data is sourced from publicly available mod CPP files
