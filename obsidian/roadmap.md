---
tags: [honeymod, roadmap]
status: active
---

# Roadmap — Future Sessions

Parked tasks from Session 1, ordered by dependency and impact.

## Next session (Session 2)
1. **SMAPI smoke test** — launch the game via SMAPI; inspect console for red errors; fix any missing asset / format issues.
2. **Map the intro event tile coordinates** — verify Farm path coords (34,13)–(34,16) are passable on multiple farm types; adjust if any farm path mismatch.
3. **Personalize** — swap placeholder name/gift preferences/dialogue with real girlfriend details.

## Subsequent
4. **Custom HoneyNook location** — add via `Data/Locations` (SDV 1.6 built-in method) + small Tiled `.tmx` map; place warp tiles on vanilla `Maps/Forest` or `Maps/Town`.
5. **Real pixel art** — replace `assets/characters/Honey.png` (64×512, 4-col layout) + `assets/portraits/Honey.png` (128×384, 6-portrait grid). Photo-to-pixel conversion → manual polish.
6. **Additional festival events** — Flower Dance, Dance of Moonlight Jellies, Feast of Winter Star; needs `Set-Up_additionalCharacters` / `MainEvent_additionalCharacters` patches and festival dialogue.
7. **C# framework mod** (separate SMAPI mod folder `HoneyMod.Framework`, UniqueID `Ihimiwen.Framework`) — custom logic as needed: advanced cutscene camera, date-night minigame, custom items beyond vanilla, spouse room reskin.

## Content to add / refine
- Additional daily dialogue for all four seasons (currently Mon–Sun are generic).
- HoneyNook interactable objects (bookshelf, honey jar, bench).
- Custom item: "Her Book" (`Data/Objects`) with a description that's a direct love letter.
- Engagement dialogue customization beyond the two slot keys.
- Flowers Dance dance sprite frames (female frames 40–47 in sprite sheet).
- Kissing sprite: set `KissSpriteIndex` to 28 and `KissSpriteFacingRight` to true (default for any non-vanilla female NPC).

## Packaging
- Zip `HoneyAnniversary.zip` containing the mod folder only (strip `obsidian/`, `opencode.jsonc`).
- Include a one-page `README.txt` for her (non-technical, tells her how to install, what to expect, hidden easter eggs).