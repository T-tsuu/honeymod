---
tags: [honeymod, project, overview]
status: active
---

# HoneyMod — Project Overview

Anniversary gift mod for Stardew Valley (SDV). Emotional core: "She writes me a book, I write her into the game." 1-year anniversary gift.

## Goal
A playable Stardew Valley mod where a new romanceable NPC ("Honey") retells our relationship through the game: daily dialogue, heart events, letters, marriage. The girlfriend should be able to open the game, meet a version of herself, and read our story back.

## Locked Decisions
| Decision | Value |
| --- | --- |
| Engine | Content Patcher content pack only (no C# yet) |
| NPC internal name | `Ihimiwen_Honey` (prefix = mod UniqueID `Ihimiwen`) |
| NPC display name | "Honey" (i18n key `npc.displayname`) |
| Marriageable | Yes (`CanBeRomanced: true`) |
| Birthday | **Summer 27** (no vanilla collision) |
| Author | Casanova |
| UniqueID | `Ihimiwen` (note: distinct from existing `Casanova.Ihimiwen` village mod in Mods) |
| CP Format | `2.8.0` (installed Content Patcher is 2.8.1) |
| Future C# | Planned as a SECOND mod folder (`HoneyMod.Framework`, EntryDll), kept separate from this pack |

## Architecture
- All content = JSON patches in `content.json` targeting vanilla 1.6 data assets.
- **All player-facing text** lives in `i18n/default.json` (edit there to customize the gift).
- Art is placeholder until real pixel art is done (sprite/portrait PNGs get swapped with zero config changes).

### File tree (mod root = repo root `C:/Users/dell/Desktop/honeymod`)
```
content.json                # every patch
manifest.json               # Author Casanova, UniqueID Ihimiwen
i18n/default.json           # ALL dialogue/events/mail text
assets/
  characters/Honey.png      # overworld sprite, 64x512 = 4 cols x 16 rows of 16x32
  portraits/Honey.png       # portraits, 128x384 = 6 x 64x64 (neutral/happy/sad/blush/love/angry)
  dialogue.json             # empty base asset (entries added via EditData)
  marriagedialogue.json     # empty base asset
  schedule.json             # daily + marriage schedules
```

## What "Complete" Looks Like (definition of done)
1. Mod loads green in SMAPI log (no red errors).
2. Honey spawns and walks the valley; gifts work; birthday shows Summer 27 on the calendar.
3. 7 heart events play in order (intro → 2/4/6/8/10-heart → post-marriage anniversary night).
4. Bouquet + mermaid pendant + wedding work (vanilla mechanics).
5. Real pixel art of the girlfriend replaces the placeholders.
6. Custom date-spot location (HoneyNook) added via SDV 1.6 `Data/Locations` + TMX map.
7. (Future) C# framework mod adds any custom mechanics.

## Install / Test Quick Reference
- Copy mod folder into `Steam/steamapps/common/Stardew Valley/Mods/`; launch via SMAPI.
- Test commands (SMAPI console):
  - `debug friendship Ihimiwen_Honey 2500`
  - `debug ebi Ihimiwen_Honey` (play heart event)
  - `debug mail Ihimiwen_HoneyIntro`
  - `debug warp Beach`
  - `debug warp Farm` (triggers intro event day 2+)
- Key heart-event preconditions: intro = on Farm after day 2; 2-heart = Beach afternoon; 4-heart = Beach night; 6-heart = Beach afternoon; 8-heart = Beach morning; 10-heart = Beach night; anniversary night = Farm night while married.

## Background / Research Notes
- SDV 1.6 changed `Data/Characters` to a JSON model (fields: `DisplayName`, `BirthSeason`, `BirthDay`, `HomeRegion`, `CanBeRomanced`, `Home[]`, ...). Not the old disposition string.
- Dialogue asset names moved: `Characters/Dialogue/<name>`, marriage dialogue `Characters/Dialogue/MarriageDialogue<name>`, schedules `Characters/schedules/<name>`.
- Vanilla overworld sprite sheets are 4 columns wide (64 px), rows of 32 px. Frames indexed row-major: row 0 = down, 1 = up, 2 = left, 3 = right (4 frames each).
- Custom locations are now done via `Data/Locations` (CP `CustomLocations` is deprecated).