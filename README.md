# The Last Apothecary Final Demo

A self-contained HTML5 side-scrolling action-platformer. The browser game contains its JavaScript, CSS, room data, pixel-art rendering, sound synthesis, saves, menus, upgrades, enemies, and boss. It requires no server, npm packages, external images, or runtime downloads.

## Play the game

1. Download and extract the project ZIP.
2. Open `index.html` in Chrome, Edge, Firefox, or another modern desktop browser.
3. Audio starts after your first key press. Browser storage is used for checkpoints, progression, and achievements when available.

The HTML file linked separately as **The Last Apothecary Final Demo.html** contains the same full standalone game code as the project's `index.html`.

## Controls

| Input | Action |
|---|---|
| A / D or Left / Right | Move |
| Space or Up | Jump; hold for a higher jump |
| J | Strike |
| Q | Mend when safe and with enough reagent |
| K or Shift | Dash after finding the dash upgrade |
| L | Throw a vial after finding the vial upgrade |
| E | Interact with levers, treatment stations, and objects |
| M | Open or close the map |
| Esc | Pause or resume |
| Up / Down + Enter | Navigate title/pause menus (Up moves upward) |
| B | Open achievements during play |
| Left / Right, A / D, or Page Up / Page Down | Change achievement pages |
| Mouse click | Choose a pause-menu button |
| N | Toggle sound |
| V | Toggle screen shake |
| F2 | Toggle debug display |

## Rooms and progression

The connected world has eleven rooms: Sealed Chapel, Plague Street, Cistern Gate, Apothecary Vault, Ossuary Stairs, Root Hall, Flooded Wards, Bellkeeper's Chamber, Reliquary, Risk of Rainfall, and The Pale Burrow. Find the dash upgrade in the Vault, use the Root Hall lever to open the high Chapel gate, recover the spare mask in the Reliquary, and defeat the Bellkeeper.

The two Easter egg rooms are deliberately hidden. Drop through the moss-veiled floor break in Flooded Wards to find Risk of Rainfall. The return hatch lands on safe ground past the hole. In Ossuary Stairs, look for a faint vine seam and hold Up/W to climb; press E at its upper end to reach The Pale Burrow. Its return also uses a hidden vine seam. The map only draws the dotted secret connector after both rooms have been discovered.

The game includes one-way wooden platforms (grid value `3`). They allow upward and horizontal passage but support downward landings, while continuing to block line of sight and projectiles. Platform artwork uses weathered boards, iron nail pixels, cracks, and subdued room-colored moss. The first Sealed Chapel platform remains solid, while higher steps and the specified Plague Street/Ossuary stairs use one-way platforms. Root Hall's lower stairs remain solid, with a safe floor dip providing the alternate route underneath.

## Achievements

There are ten achievements, shown five at a time in a readable, high-contrast screen. Use Left/Right (or A/D, Page Up/Page Down) to switch pages.

| Achievement | Requirement |
|---|---|
| A Better Way | Recover the dash relic from the Vault. |
| Root of the Problem | Open the sealed Chapel gate. |
| A Second Chance | Find the spare mask in the Reliquary. |
| A Distant Downpour | Discover Risk of Rainfall. |
| Quiet Beneath the Roots | Discover The Pale Burrow. |
| Silence the Bell | Defeat the Bellkeeper. |
| Untouchable | Defeat the Bellkeeper without taking HP damage during the boss fight. |
| One Life, One Cure | Defeat the Bellkeeper without dying during the boss fight. Taking damage is allowed. |
| Flawless Formula | Finish the entire demo without taking damage. |
| A Life Preserved | Finish the entire demo without dying. Taking damage is allowed. |

The final two awards unlock only when the ending sequence completes after the Bellkeeper is defeated. Full-demo run statistics start fresh with **New Game** and persist across rooms, checkpoints, and save/reload. Damage disqualifies Flawless Formula; each death disqualifies A Life Preserved. The two earlier challenge awards are boss-fight-specific. Older saves without boss-fight history cannot retroactively qualify for those two boss-only awards. Achievement unlocks are stored in a lifetime ledger and survive starting a new game.


## Achievement catalogue

The ten achievements are split into six progression milestones, two boss-fight challenges, and two complete-demo challenges.

- **Untouchable** — defeat the Bellkeeper without HP damage during the boss fight.
- **One Life, One Cure** — defeat the Bellkeeper without dying during the boss fight.
- **Flawless Formula** — finish the entire demo without taking damage.
- **A Life Preserved** — finish the entire demo without dying.

The full-demo awards unlock only at the ending after the Bellkeeper is defeated. Their statistics begin with New Game and remain valid through room changes, checkpoints, and reloading. These four challenges are distinct: the first two assess only the boss encounter; the last two assess the entire playthrough.

## Run diagnostics

Node.js is only needed for tests, not for playing the game. From the project root run:

```sh
node tests/run.js
```

The tests parse the embedded JavaScript and exercise platform rules, locked gates, room connections, key movement through the actual `step()` loop, checkpoint/save persistence, boss boundaries, all ten achievements, and the known timing divergence. Traversal scenarios disable enemies where necessary to isolate geometry and unlock dash for routes that require it; they are not a full unassisted playthrough or combat-balance certification. Results are recorded in `TEST_RESULTS.txt`, and room links are documented in `ROOM_REACHABILITY_REPORT.md`.

## GitHub: copy and publish

### Copy-paste the complete browser game

1. Open the downloaded standalone HTML file in a text editor such as VS Code or Notepad (do not copy the rendered browser view).
2. Select and copy the entire file contents.
3. On GitHub, create a repository and choose **Add file → Create new file**.
4. Name the file `index.html`, paste the full HTML source, and commit it.
5. For the complete project, instead upload the extracted ZIP contents, preserving `tests/` and `ports/` folders.

### Publish with GitHub Pages

1. Put the project files at the repository root so `index.html` is in the root directory.
2. Open **Settings → Pages** in the GitHub repository.
3. Choose deployment from the branch and root directory (or the workflow you prefer), then save.
4. Open the published URL and test input, pause/menu behavior, and browser storage.

`HOSTING.txt` contains the same quick-start steps. No build step is necessary for the browser edition.

## Unity and Unreal starter files

`ports/unity/` and `ports/unreal/` include native-engine starter source and setup notes. They are source-only prototypes, not complete ports of every browser room and mechanic, and have not been compiled in their target editors. The full playable game delivered here is the browser HTML5 edition.

## Recovery and limitations

This is a best-effort reconstruction based on the available Edit 4 HTML and documented Edit 5 changes. The original `fix.html`, walkthrough planner, original regression suite, original reachability suite, and previously mentioned Unity files were unavailable, so this is not a byte-for-byte recovery of those missing files. A planner calling `updP()` directly still bypasses hitstop in `step(dt)`, producing an approximately 28.33 px position difference in the supplied six-frame test state; a future planner should advance frames through `step(dt)` and preserve hitstop, held keys, pressed-key edges, transitions, and fade state. No license is included because the intended license and rights to all included source/assets have not been confirmed.

