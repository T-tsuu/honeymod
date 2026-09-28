# AGENTS.md — HoneyMod (Anniversary Gift Mod)

> Multi-session project. All design docs live in the Obsidian vault inside this repo
> (the vault is dedicated to HoneyMod, so every note lives at the vault root).
> **Project hub:** `obsidian/project-overview.md`
> **Roadmap:** `obsidian/roadmap.md`
> **Session logs:** `obsidian/sessions/`

---

## File tree

```
content.json                # CP patches (Format 2.8.0)
manifest.json               # Author: Casanova / UniqueID: Ihimiwen / CP content pack
i18n/default.json           # ALL player-facing text (edit here, never hard-code in content.json)
assets/
  characters/Honey.png      # overworld sprite — 64x512, 4 cols × 16 rows of 16x32 px
  portraits/Honey.png       # dialogue portraits — 128x384, 6x 64x64 (neutral/happy/sad/blush/love/angry)
  dialogue.json             # empty base dict (entries added by content.json EditData)
  marriagedialogue.json     # empty base dict
  schedule.json             # pre-marriage schedule (BusStop + Beach) + marriage (FarmHouse)
```

> **Do not** commit `obsidian/`, `opencode.jsonc`, `_mcp_probe.md`, or any `*.py` scratch scripts.

---

## Sessions

| # | Date | Status | Log | Summary |
|---|------|--------|-----|---------|
| 1 | 2026-09-14 | **completed** | `obsidian/sessions/2026-09-14-session-1.md` | Built full playable scaffold: all data patches, 7 heart events, 6 letters, placeholder art, validated JSON + PNG specs. |

---

## Coding conventions

| Rule | Detail |
|------|--------|
| Format version | `"Format": "2.8.0"` (matches installed CP 2.8.1) |
| UniqueID / prefix | `Ihimiwen` — all asset names must use `Ihimiwen_Honey` |
| Text / i18n | Every dialogue line and mail text belongs in `i18n/default.json` (keyed `dialogue.*`, `events.*`, `mail.*`, `marriage.*`, `gift.*`). Use `{{i18n: <key>}}` tokens in `content.json`. |
| Sprites | `assets/characters/Honey.png` must be exactly **4 columns × 16 rows of 16×32 px** (64×512 total). Frames: row 0 = down, 1 = up, 2 = left, 3 = right (4 frames each). Kiss frame = index 28. Flower Dance female frames = 40–47. |
| Portraits | `assets/portraits/Honey.png` must be **128×384** (6 × 64×64 cells). Order: `$0` neutral, `$1` happy, `$2` sad, `$3` unique/blush, `$4` love, `$5` angry. |
| Events | Unique string IDs prefixed `Ihimiwen_Honey_*`. Use `!FestivalDay` in Beach events. |
| Gift tastes | `/`-separated 10-segment string. i18n tokens must never contain `/` (breaks parsing). |
| Marriage schedules | `marriage_Mon`..`marriage_Sun` keys in `assets/schedule.json`. Spouse stays in `FarmHouse 3 4 2` (living room; cosmetically fine, fails gracefully). |
| Deployment | Copy only mod files into `Mods/` — exclude `obsidian/`, `.py`, `_mcp_probe*`, `AGENTS.md`. |

---

## How to run tests / validate

```bash
python validate_mod.py   # C:/Users/dell/AppData/Local/Temp/opencode/validate_mod.py
```

In-game (SMAPI console):
```
debug friendship Ihimiwen_Honey 2500
debug ebi Ihimiwen_Honey
debug mail Ihimiwen_HoneyIntro
debug warp Beach
```
