# Mini World: CREATA — World save `w30396532858891`

> 🇻🇳 [Tiếng Việt](README.vi.md) · [Đóng góp / CONTRIBUTING (tiếng Việt)](CONTRIBUTING.md)

Project files for a **Mini World: CREATA** map, stored exactly as the game writes them.
This repository is the world folder itself — so "updating the map" simply means copying
the folder the game just saved and pushing the diff.

## Map metadata

| Field | Value |
| --- | --- |
| World folder / ID | `w30396532858891` (world ID `30396532858891`) |
| World name | `Độc tày SangsDayy` |
| Author | SangsDayy (UIN `1049305099`) |
| Game | Mini World: CREATA |
| Save version | `1.7.15` |
| Description | `Currently under development` · `Hát [W.I.P]` |
| Built-in notes | In-game "Danh sách lệnh" (command list), stored in `wglobal.fb` |

## Commands shipped with the map

Taken from the map's own in-game notes.
`<...>` = value required · `[...]` = optional.

| Command | Who can use it |
| --- | --- |
| `/buff <buff_id> <buff_level> [tick_time]` | Everyone |
| `/clearbuff <buff_id\|all>` | Everyone |
| `/tpa <player_id>` | Everyone |
| `/size <value>` | Everyone |
| `/money view [player_id]` | Everyone |
| `/kill [player_id]` | Room owner |
| `/fly [player_id]` | Room owner |
| `/give <item_id> <count> [player_id]` | Room owner |
| `/tp <player_id\|pos>` | Room owner |
| `/god [player_id]` | Room owner |
| `/perm <permission> <player_id\|all> <on\|off>` | Room owner |
| `/perm view <player_id>` | Room owner |
| `/revive <player_id>` | Room owner |
| `/summon <mob_id\|name> [pos\|player_id]` | Room owner |
| `/tree <name\|id\|random> [player_id] [seconds]` | Room owner |
| `/antivoid` | Room owner |
| `/attr set\|add\|remove <id\|all> <attr> <value>` · `/attr view <id>` | Map owner |
| `/money <add\|set\|remove> <player_id\|all> <value>` | Map owner |
| `/skybox` | Map owner |
| `/worldedit` | Room owner / Map owner |

`/skybox` and `/worldedit` are defined in encrypted trigger scripts
(`ss/trigger/game_type_1/script_179093296101.lua` and
`ss/trigger/game_type_1/script_179094651701.lua`), so their exact syntax is not documented here.

Permission bits used by `/perm`:

| Permission | ID | Permission | ID |
| --- | --- | --- | --- |
| `move` | 1 | `beattacked` | 64 |
| `place` | 2 | `bekilled` | 128 |
| `operate` | 4 | `pickup` | 256 |
| `destroy` | 8 | `drop` | 512 |
| `use` | 16 | `vehicle` | 1024 |
| `attack` | 32 | `discard` | 2048 |

## Custom NPCs

Three NPC actors live in `mods/mapdefault_0.1_*/behavior/actor/`. Those JSON files are
plain text, so everything below was read straight out of the repository.

| Actor ID | File | Name | Purpose | HP |
| --- | --- | --- | --- | --- |
| `100000` | `1790917867.json` | Lão Bạch | Fishing — hands out the starter rod, and upgrades / repairs rods | `1200` |
| `100001` | `1790918605.json` | Báo Tuyết | Sells fish for money | `1200` |
| `100002` | `1790918662.json` | Đường Khả Hinh | Sells tickets | `150` |

`mods/allocatedidid.json` allocates an actor ID and a matching item ID to each NPC
(items `4098`, `4099`, `4100`).

## Repository layout

| Path | Contents |
| --- | --- |
| `m0/`, `m1/`, `m2/` | World chunk data — `x<X>z<Z>.r` regions plus `a<X>_<Z>.a` sidecars. `m1/` and `m2/` are empty (unused dimensions). |
| `sandbox/nodes/` | Sandbox map binaries: map data, save, config, scene, CRC checksums. |
| `scenetree/scene/` | Scene descriptor `<worldId>_MapDefault.uscene` (a ZIP container). |
| `ss/` | Script system — `config.lua`, `trigger/**` Lua trigger scripts, `vardata/` variable stores. |
| `visualcode/` | Visual-code (block) editor state — `actor.db`, `function.db`, `trigger.db`, `variable.db`, `custommsg.db` and the generated `workspace/**` Lua. |
| `customui/` | Custom UI projects (`.proj`, triggers, per-project visualcode). |
| `custommodel/`, `custommotion/`, `custompic/` | Custom model / motion / picture assets, each with its own `manifest.mf`. |
| `mods/` | Default behaviour pack — 3 blocks (`GrassBlock`, `PeachLeaves`, `Sand`), 1 item, the custom NPCs above, and the ID-allocation table `allocatedidid.json`. |
| `modpkg/` | Installed pack manifests plus its own `ss/` variable store. |
| `blueprint/`, `vbp/` | Blueprints (`.bp`) and blueprint descriptions. |
| `roles/` | Per-player role/permission files, named `u<UIN>.p`. |
| `string/` | Localised string tables. |
| `objlibs/`, `vehicle/`, `tradeCaravanData/` | Object library, vehicle data, trade-caravan data. |
| `wdesc.fb` | World metadata — name, author, description, version. |
| `wglobal.fb` | World-wide data, including the JSON command-list notes. |
| `wsize.fb`, `wterrtype.fb`, `wmultilang.fb` | World size, terrain type, multilanguage settings. |
| `cover.data`, `thumb.png_` | Cover image metadata and thumbnail. |
| `resourceList.data`, `CoustomAvator.json` | Encoded resource list and custom avatar. |
| `triggerarea.fb` | Trigger / teleport area definitions. |
| `UserConfig/`, `transfer/`, `starstationtransfer/` | Empty runtime folders — the game recreates them. |

## File formats

Most files are **not** plain text. The game encrypts or encodes them:

- `.ex` files ship with an `*_ex_desc_` sidecar describing the scheme —
  `{"encrypFlag":"xxtea_64","compressFlag":"none","serializeFlag":"json","version":...}`.
- `.uscene` files are ZIP archives whose `desc.json` entry is password-protected.
- `.lua`, `.db`, `.fb` payloads are base64-wrapped ciphertext (the `v1633` prefix on
  `.db` files is a format tag, not encryption).

Readable without tooling: `mods/**/*.json`, the `pack_manifest.json` files, the
plaintext portions of `wdesc.fb` / `wglobal.fb`, and the `.gitignore` rules.

## Updating the map

> [!IMPORTANT]
> Copy the game's world folder **over** this one, never delete-then-copy.
> Deleting first would wipe `README.md`, `README.vi.md`, `CONTRIBUTING.md` and `.gitignore`.

1. Play/edit the map in Mini World, then leave the map so the game finishes writing files.
2. Locate the world folder on your device (it carries the same name as this repo).
3. Copy its contents into your local clone, keeping `.git/`, `README.md`,
   `README.vi.md`, `CONTRIBUTING.md` and `.gitignore`.
4. `git status` — review what changed.
5. `git add -A && git commit -m "<what changed>"`.
6. `git push`.

Files matching `.gitignore` (temp folders, `*.uinError`, UIN snapshots, log files)
are skipped automatically — `git status` should never list them.

Full step-by-step instructions, including a no-git-experience walkthrough, are in
[CONTRIBUTING.md](CONTRIBUTING.md) (Vietnamese).

## Cleaned-up artifacts

The following were removed from the repository because the game regenerates them
and they only add noise to the history. They are still recoverable from older commits.

| Removed | Why |
| --- | --- |
| `modpkgtmp/` | Partial duplicate of `modpkg/`. |
| `ss/vardata/tmp/`, `modpkg/**/vardata/tmp/` | Stale variable cache, older than the live copies. |
| `wdescbackup.fb`, `thumb_temp.fb` | Explicit backup / temp world files. |
| `visualcode/**/*.uinError`, `visualcode/**/*.db.<uin>` | Empty error markers and per-UIN snapshots from failed loads. |
| `scenetree/scene/<otherId>_MapDefault.uscene` | Scene descriptors belonging to other worlds. |
