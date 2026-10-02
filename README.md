# Session Lobby

A full-screen, customizable landing page for Foundry VTT (v13–v14). Everyone sees it while the session isn't running; the GM presses **Start Session** and it fades away for the whole table.

## Install
Unzip into `Data/modules/` so you have `Data/modules/session-lobby/module.json`, then enable **Session Lobby** in your world.

## Themes
Each layout picks a theme when you create it (**+** in the designer):
- **Clear Sky** — bright notebook style with polaroids, quote bubble and real-world clock.
- **Grimoire** — fantasy library: pointed side banner with your campaign name, top nav bar, torn-parchment hero, party panel, image cards (current arc / recent session / upcoming…), quick links, a **music player** and an **in-game calendar**.

Every image slot in Grimoire is yours to fill: background (image or video), character art, banner crest, banner bottom image, card images, party portraits, music cover art, and an optional parchment texture.

### In-game calendar (Grimoire)
Pick where the date comes from in *Calendar & Music*:
- **Foundry's calendar** — follows world time and whatever calendar your system uses (dnd5e's Harptos, Greyhawk…). Day/Year adjust fields fix any off-by-one.
- **My own months** — type months (`Name: days`) and weekdays; driven by world time.
- **Manual** — just type the day, month, year and time.
Click the calendar to see the month grid; the GM gets −1h / +1h / +8h / +1 day buttons there (they advance Foundry's world time).

### Music player (Grimoire)
Shows the track and playlist currently playing in Foundry with a progress bar. The GM gets previous / play-stop / next buttons (drag a Playlist into the designer to choose what Play starts). Everyone gets a volume slider that controls their own music volume.

### Character art slideshow (both themes)
Under *Look → Slideshow*, add as many character images as you like — they crossfade on a timer. Set seconds per image, fade length, random order, and per-image size/nudge so differently-sized PNGs line up. **Add every image in a folder** imports a whole folder at once. One image = a still picture.

## World Map
An interactive map players can explore from the lobby (the Grimoire **Map** nav item and **World Map** quick link open it by default; any button can use *Open the World Map*).

- **Players:** drag to pan, scroll to zoom, click a region to fly into it. The rest of the map dims, the region's waymarks appear, and the side panel lists them as buttons. Clicking a waymark opens its journal/page/scene/note. **Esc** zooms back out, then closes.
- **Set up (GM):** open the map → **Edit map** → *Choose image*. Then:
  - **Draw region**: click corners; click the first corner, double-click or press Enter to finish.
  - **Box region**: drag a rectangle.
  - Pick a color from the palette (or any custom color), name it, give it a description (shown when players open it; `@UUID` links work).
  - **Waymark**: zoom into a region first and click to place a waymark inside it. At the whole-map level, waymarks become landmarks that are always visible.
  - Drag a journal, page, scene, actor or macro onto a waymark's *When clicked* box to link it, or choose *Pop-up note* and write text.
  - **Select** tool: drag waymarks or region corners to adjust; right-click a corner to delete it.
  - Regions and waymarks can be **hidden from players** until you're ready to reveal them.
- Edits save automatically; players see them when you click **Done editing**.
- Macro: `game.modules.get("session-lobby").api.map()` (or `.map(zoneId)` to open straight into a region). There's also an optional keybinding.

## Shops (Stylish Shop integration)
Requires the **Stylish Shop** module (premium, by GlitchSmith). If it isn't active, the Shops features stay hidden and buttons just show a notice.

- **Shops window:** any lobby button or map waymark set to *Open the Shops list* (new Grimoire layouts include a **Shops** banner link).
  - **Players** see only the shops that are open right now, grouped by town, and click **Enter** to shop in Stylish Shop's own interface.
  - **GM** sees every shop with an **Open/Closed** switch, can group shops into **towns** and open or close a whole town at once, or **Close every shop**.
- **"Open" = remote shopping on.** This uses Stylish Shop's own *public shop* setting, so open shops can also be browsed from Stylish Shop's Shop Directory. Only shops you toggle in this window are managed; shops you made public yourself in Stylish Shop are left alone.
- **Between sessions only (default on):** while a session is live, open shops close automatically and show *Waiting*; they reopen when you return to the lobby. Untick it in the Shops window to keep shops open during play.
- **One specific shop:** set a button or waymark to *Open one Stylish Shop* and drag the shop's actor onto it. If that shop is closed, players are told so.
- **Token:** `{shops}` = number of shops open right now (e.g. a card badge "{shops} open").
- Purchases are approved by the GM through Stylish Shop, so players can browse while you're offline but can only buy while you're online.

## Quest Log & Relationship Tracker buttons
Any lobby button or map waymark can open these (they show a notice if the module isn't active):
- **Open the Quest Log (Quest Board):** opens only the Quest Log, not the board. While the lobby is showing, players won't see the log's own "Quest board" button (turn that off in Module Settings → *Quest Log from the lobby: hide its Quest Board button*).
- **Open the Relationship Tracker:** choose what it opens:
  - *Character picker* (the tracker's normal start).
  - *My character's relationships*: the player's assigned character; falls back to the picker if they have none.
  - *A specific character*: drag an Actor onto the button.
  - *Organizations / factions*.
- Macros: `api.questLog()`, `api.relationships("mine")`.

## Party Vault
A shared party inventory with coins. Players can **see it and deposit only from the lobby**, and can **withdraw only at a bank**.

- **First time (GM):** open the vault (any lobby button set to *Open the Party Vault*; the Grimoire "Item Vault" link uses it by default) and click *Create a "Party Vault" actor*, or drag your party Group actor onto the window. New vaults are hidden from players, so the vault window is the only way in.
- **Lobby (players):** view funds, items and the ledger; deposit items (drag them in) and coins. Withdraw and Take are locked.
- **Bankers (GM):** drag any NPC onto the vault window to make them a banker. Set *Reach* (empty squares allowed between tokens; 0 = adjacent).
- **At the bank (players):** during the session, when a token you own stands within reach of a banker's token on the scene you're viewing, a **Visit the bank** button appears. Withdrawals and taking items unlock there, and lock again when you walk away.
- **Open the bank for everyone (GM):** one click lets everyone withdraw without tokens (theater of mind); click again to close it.
- **Enforcement:** player changes go through the GM's client, which checks the bank rules before doing anything, so **a GM must be online** for players to deposit or withdraw. If the vault actor is still owned by players (e.g. made with v1.2.0), the vault window shows a **Lock it** button.
- **Coins:** pick a character, type amounts, Deposit/Withdraw. Coins move between the character and the vault; overdrafts are refused. The GM also has *Vault only* to adjust funds directly.
- **Ledger:** every deposit/withdrawal/take is logged with who did it.
- After installing v1.2+, **return to Setup and relaunch the world once** — Foundry only enables a module's network messaging at launch.

## Using it
- **Design it:** click **Design** on the lobby's toolbar (top center, hover to reveal), or *Game Settings → Configure Settings → Session Lobby → Open Designer*. Changes preview live; hit **Save** to push them to players.
- **Start / end the session:** **Start Session** on the lobby, the door icon in the token controls, or **Ctrl+Shift+L**. While a session is live, the toolbar shows **Back to Lobby (all)**.
- **Players** can minimize the lobby to a small "Open Lobby" pill (turn this off in Clock & Music → Players), and can peek at it mid-session with Ctrl+Shift+L.

## What's customizable
| Area | Options |
|---|---|
| Header | Logo image or icon, title, subtitle, two meta lines, badge, vertical side text, footer |
| Hero | Section number/label/tag, two-line headline (line 2 is highlighted), tagline, info chips |
| Buttons & Cards | Big call-to-action, small buttons, bottom cards — add/remove/reorder any number |
| Party & Quotes | Polaroids (drag an Actor in to fill name + portrait; link a player for an online dot), rotating quote bubble |
| Clock & Music | Date, weather, live clock, next-session countdown, attendance ticks, now-playing from your playlists |
| Look | Colors, fonts, notebook lines, background image **or video**, character art position/size/flip |

Every button can: show a pop-up note (HTML + `@UUID` links), open a Journal / Journal Page, Actor, or Item, run a Macro, pull everyone to a Scene, open a web link, or start the session. Drag a document from the sidebar onto a button's **Linked document** box. Permissions are respected — players only open what they can see.

Text fields accept live tokens: `{date} {longDate} {time} {countdown} {dday} {nextDate} {online} {total} {world} {music}`.

**Multiple layouts:** keep several lobbies (e.g. one per arc) and pick which is live with the ★ button. Export/Import JSON to share them.

## Notes
- Foundry only lets players connect while the world is launched, so this is the screen they land on between login and the GM starting play.
- The stage is designed at 1920×1080 and scales to fit any window.
- Enable "Keep the chat sidebar visible" if you want people chatting in the lobby.
- Macro API: `game.modules.get("session-lobby").api` → `open()`, `close()`, `startSession()`, `endSession()`, `designer()`.
