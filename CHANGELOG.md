# Changelog

All notable changes to Threat Ledger are recorded here.
Bug reports: https://github.com/HiDanny666/ThreatLedger/issues

The format follows [Keep a Changelog](https://keepachangelog.com/), and versions use
[semantic versioning](https://semver.org/).

---

## [0.3.1] - 2026-10-26

Compatibility with RimWorld Together (`nova.rimworldtogether`, Workshop 3005289691).

### Added

- **RimWorld Together transfers in the trade threat panel.** Player-to-player trading in
  RimWorld Together uses its own windows instead of `Dialog_Trade`, so the panel did not open
  for them. It now opens beside both:
  - the **transfer window** (what you send): every row set to "Offer" is a "Send" line. RimWorld
    Together always sends whole stacks, and a pawn leaves with everything they wear and carry,
    taking their pawn points with them;
  - the **transfer request** (what another player sends you): every thing is a "Receive" line,
    landing on the home map (gift / drop pod) or in your caravan (the answer to your own caravan
    trade). While you answer a trade request from your settlement, the panel shows the whole
    exchange: what you send and what you will receive.

### Fixed

- Mod detection now also finds Workshop copies listed with the `_steam` suffix (this happens
  when a local copy with the same package id exists). Applies to RimWorld Together and to
  Multiplayer (Multiplayer was still found through its fallback check before).

### Notes

- RimWorld Together is not lockstep: every player runs their own game. Threat Ledger stays
  read-only (no Harmony patches, nothing spawned or destroyed, random state restored), so it
  never touches anything RimWorld Together syncs, including its synchronous-visit patches.
  Events another player sends you (raids included) are sized by RimWorld Together with
  `StorytellerUtility.DefaultParmsNow` on your map, i.e. your own threat points - exactly the
  number on the dashboard.

---

## [0.3.0] - 2026-10-26

Trading, adding items and crops: three new ways to ask "what would this do to my next raid?",
and correct numbers for every player faction in Multiplayer.

### Added

- **Trade threat impact panel.** When a trade window opens (caravan, orbital trader,
  settlement - vanilla `Dialog_Trade` or Multiplayer's `TradingWindow`), a panel opens beside
  it on its own. As counts change it shows the threat after the whole deal, wealth gained /
  lost, pawns joining / leaving, and for **every bought or sold row** its wealth change and
  how many points it adds or removes (hover for the per-unit effect). Silver is its own row.
  It follows what the game really does: bought things arrive as items (minified buildings too),
  bought colonists or slaves add pawn points and bring their gear, a sold colonist leaves their
  weapon and inventory behind and takes their clothes, a sold prisoner's dropped gear becomes
  colony items; from a caravan everything is counted "as if brought home". Close it with its X
  (stays closed until that trade ends) or switch it off in the settings.
- **Add-items simulation ("+ Add" in the what-if drawer).** Search any of the ~1,100 items and
  player-buildable buildings, click to add, then set count, material and quality. Items count
  in full, buildings as installed (half value). Combines with the ticked removals; the result
  card now shows wealth removed, wealth added and wealth afterwards.
- **Crop harvest estimate.** "Harvest: ready now" and "Harvest: all grown" turn the colony's own
  crops (sown plants, hydroponics basins, plant pots) into the produce they would give, using
  the game's yield formula (growth, plant damage, difficulty crop yield) without its random
  rounding.
- Help page sections: adding items, **how crops count** (growing plants are not wealth at all;
  only harvested produce counts), trade threat impact.
- Setting: *Show the "trade threat impact" panel while trading*.

### Fixed

- **Multiplayer with Multifaction:** looking at another player faction's colony priced it with
  *your* storyteller, difficulty and adaptation and found none of its pawns (Multiplayer keeps
  these per faction). The panel, the trend sample and the what-if list now read that map as its
  owner, through Multiplayer's own `PushFaction` / `PopFaction`, restored in the same frame.
  A note says when this happens.

### Changed

- Small changes show one decimal (`+0.4` instead of `0`) in the trade panel and the add list.
- "Clear ticks" is now "Clear all" (it also clears planned additions).

### Compatibility and testing

- Tested in game with Multiplayer 0.11.5 + MP Desync Fixes v0.3.3 (Multifaction and async time),
  including 50,754 ticks at top speed next to the arbiter with the tab, drawer and additions
  open: no desync. Tested with Combat Extended. Still no Harmony patch, no game component and
  nothing in the save: the trade panel is opened by a small Unity object that polls the window
  stack four times a second (0.04 us per frame when no trade is open).
- 25 new unit assertions (161 total) and 31-39 in-game checks per variant; predictions match the
  game exactly after really adding gold, walls, produce and executing a trade.

## [0.2.1] - 2026-10-20

### Fixed

- Help & notes: long notes (for example the 1M wealth plateau in Chinese) wrapped past
  their row and were clipped; each row is now as tall as its text.
  Checked in game.

### Added

- RimWorld **1.7** is now listed in the supported versions, alongside 1.6.
- Steam Workshop cover image (`About/Preview.png`).

## [0.2.0] - 2026-10-20

The interface is rebuilt from scratch and the formula is now read from the game in full.

### Changed

- **New dashboard interface.** The five tabs (Overview / Wealth / Formula / What-if / Notes)
  are replaced by one page: a headline card (game value, status badge, 1-day change, raid
  estimate), a formula waterfall, three wealth cards, a threat trend chart, and a what-if
  drawer that slides up from the bottom. Help & notes and Settings are buttons in the header.
- **The formula is reproduced exactly.** Adaptation (softened by the difficulty's
  adaptation effect), the storyteller's new-colony factor and the difficulty floor are read
  from the game, and every player pawn is priced the way `StorytellerUtility` prices it:
  colonists by the wealth curve, release-trainable animals at 8% of combat power, colony
  mechs and subhumans at 20-40% of combat power, then health, slavery (x0.75), Biotech age
  and cryptosleep (x0.3). On a vanilla game the "unexplained multiplier" disappears.
- **Reconciliation is stricter** once every factor is known: a gap above 10% (was 50%) is
  reported as another mod changing the formula.
- **Raid estimates** now weight each fighter by how often the game picks it, show one row
  per faction type instead of one per faction, and are cached instead of rebuilt every frame.
- The panel refreshes once per second (was every two seconds).

### Added

- **What-if for pawns:** colonists, slaves and children individually; animals, mechs and
  subhumans grouped by kind; removing them takes away their market value *and* their pawn
  points. Prisoners are listed with a note that they count for nothing.
- **What-if for floors** as one entry, plus filter chips (All / Items / Buildings / Pawns),
  a search box, and each row's solo effect shown next to it.
- **Threat trend chart:** one sample per in-game hour for up to 20 days, with 1-day and
  7-day change. Samples are kept in memory only and never saved. Recording can be turned off.
- Handling for **temporary maps** (camps, quest sites), **fixed-wealth difficulty**,
  **pocket maps** (evaluated as their source map, like the game does) and the **minimum /
  maximum clamp**, each with an explanatory note.
- Settings: *Show the threat trend chart*, *Record threat trend*.
- **DefInjected** translations, so the tab's own name is translated in Chinese.
- 67 new unit assertions (136 total) and a performance budget test.
- Dev mode only: a `[Threat Ledger perf]` log line every 300 frames with draw, refresh and
  scan timings, for anyone checking the mod's cost.

### Performance

Measured in game on a 1.2M-wealth colony (Dev mode timing log), with identical results:

- The what-if map scan now runs only while the drawer is open, every 10 s instead of 3 s,
  and caches unit values within a scan: ~9 ms every 3 s → ~2.8 ms every 10 s. With the
  drawer closed the panel no longer causes frame spikes (11 ms → ~2 ms max).
- Per-frame drawing: 0.32 → 0.24 ms (drawer closed), 0.43 → 0.35 ms (drawer open), by
  caching everything that only changes on refresh, building tooltips only on hover, and
  downsampling the trend line.
- Pawn market values (an expensive stat) are only read when the drawer needs them.

### Fixed

- What-if ticks were reset every few seconds when the item cache expired.
- Ticking "All items" (or "All buildings") together with one of its items counted that
  item twice.
- Buildings not owned by the player (ruins, ancient structures) and items hidden under fog
  were counted in what-if, unlike the game's own wealth.
- `DefaultThreatPointsNow` touches the random number generator through its seeded floor;
  the call is now wrapped so the generator state is restored exactly.
- Several translation errors, including a Simplified character in the Traditional Chinese
  description and the tab name staying in English.
- Found in game and fixed: raid estimate rows were clipped for Chinese text, the what-if
  "after" number could wrap onto two lines, and the item list was not in market-value order.
- Categories past the 1,000,000 wealth plateau showed 0 points with no explanation; the
  wealth cards and Help now say why.

### Compatibility

- Supported game version: **1.6** (compiled against 1.6.4871)
- Required DLC / mods: **none**
- Save files: nothing is written; safe to add or remove mid-game.
- Tested in game on 1.6.4871: breakdown matches the game exactly (drift 0.00%).
- Tested with Multiplayer 0.11.5 (host + client, about one in-game day, panel open on both
  sides): **no desyncs**.

### Known limitations

- Animations, sounds, the settings page and DLC-specific cases are not yet checked in game.
- The raid head count remains an estimate (+/-15%); raid strategy is not modelled.
- The trend chart starts again after loading a save.

---

## [0.1.0] - unreleased (superseded by 0.2.0)

First build. Never published.

### Added

- **Threat Ledger tab** alongside Work / Assign / Health.
- **Overview tab** — the game's own threat point value beside Threat Ledger's breakdown of
  it, the storyteller wealth split, and an estimated raid composition.
- **Wealth tab** — items, creatures and buildings by market value, the storyteller wealth
  each counts as, the threat points each is responsible for, and its share of the total.
- **Formula tab** — the full threat point chain line by line, including the multiplier that
  could not be read directly.
- **What-if simulator** — tick any item, building, or whole category and see the threat
  change and the resulting raid size immediately.
- **Reconciliation** — the panel detects when another mod has replaced the threat formula
  and says so, rather than silently reporting the wrong numbers.
- **Notes tab** — a plain-language explanation of where each number comes from.
- **5 panel animation styles** — numbers roll up, bars grow in, the wealth bar sweeps in,
  the formula reveals line by line, or sections fade in. Animation can be turned off.
- **5 panel sound styles** — data terminal, hydraulics, paper ledger, threat alarm, and a
  near-silent minimal click. Each is three synthesised UI sounds.
- **Mod settings** — animation style, sound style, sound toggle, and per-section toggles.
- **English, Chinese Traditional and Chinese Simplified** translations.

### Compatibility

- Supported game version: **1.6**
- Required DLC: **none**
- Required mods: **none** (Harmony is not used)
- Multiplayer (`rwmt.Multiplayer`): safe mode enabled automatically

### Performance

- Nothing executes while the tab is closed: no tick, no game component, no patch.
- The map is re-read at most twice per second while open; the item scan is cached.
- Turning off the what-if simulator removes the only map scan.

### Technical notes

- Zero Harmony patches. The mod only reads public game values.
- The threat point model is implemented as pure functions with no game references, and is
  covered by 69 assertions that run without RimWorld installed.
- Animation uses Unity's real-time clock and never consumes `Verse.Rand`, which is what
  keeps the mod safe in multiplayer.
- Binary assets (15 WAV files and 2 PNG icons) are synthesised from code, so the mod carries no third-party media.

### Known limitations

- Adaptation and the new-colony starting factor cannot be read directly, so they are
  reported together as an "unexplained multiplier" rather than being guessed.
- The what-if simulator covers items and buildings. Animals and prisoners are planned.
- The precise raid simulator (an actual dry run of the game's group generator) is not
  implemented in this version. The point estimate shown is arithmetic over faction raider
  costs.
- Read on 1.6.4850. Verification on the 1.7 Waylith beta is pending.
- Read on vanilla and with the base game's factions. Verification across a full DLC set
  and a large mod list is pending.
