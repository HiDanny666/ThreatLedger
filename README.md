# Threat Ledger

**A read-only RimWorld dashboard that shows exactly why your colony gets the raids it gets.**

RimWorld decides raid size with a hidden formula and never tells you any of it.
Threat Ledger adds one tab that lays the whole thing open — and lets you test a change before you commit to it.

> **No Harmony patches. No game state changes. Nothing in your save.**
> The random number generator is saved and restored around every read.

- **Game version:** RimWorld 1.6
- **Current version:** 0.2.0 — see [CHANGELOG.md](CHANGELOG.md) for what changed
- **Languages:** English, 繁體中文, 简体中文
- **Requires:** nothing (no Harmony, no other mods, no DLC)
- **Bug reports:** https://github.com/HiDanny666/ThreatLedger/issues

---

## Install

1. Download `ThreatLedger-<version>.zip` from [Releases](https://github.com/HiDanny666/ThreatLedger/releases/latest).
2. Unzip it into `RimWorld/Mods/`, so you get `RimWorld/Mods/ThreatLedger/`.
3. Enable **Threat Ledger** in the mod list. No load order requirements.

To uninstall, delete the folder. Nothing is stored in your save, so this is safe mid-game.

## How to get it in game

Nothing to research, build or craft. As soon as you have a colony, a **threat ledger** tab appears at the bottom of the screen next to Work / Assign / Health.

## What it shows

| Section | What it gives you |
| --- | --- |
| **The game's value** | The threat points the next raid would really use, a status badge (matches the game / small gap / another mod changed the formula), the change over the last day, and roughly how many raiders each hostile faction would send right now |
| **Formula waterfall** | Wealth points, colonists, animals and mechs add up to base points; then adaptation, difficulty and the new-colony factor multiply it; then the game's minimum / maximum. Hover any row for the exact rule |
| **Wealth cards** | Items, creatures and buildings (counted at half value): market value, what they count as, and the points each is responsible for |
| **Threat trend** | Threat points over up to 20 in-game days, one sample per in-game hour, with 1-day and 7-day change |
| **What-if simulator** | Click the bar at the bottom to slide it up. Tick items, buildings, floors, colonists, slaves, animals or mechs (filter + search) and see the new threat and raid size instantly |
| **Help & notes** | Plain-language explanation and any warnings about this colony |

## How to use it

1. **Big number, top left** — what the game will really use for the next raid.
2. **Status badge** — green means Threat Ledger's breakdown matches the game exactly. Amber is a small gap (hover for why). Red means another mod changed the formula; the big number is still correct.
3. **Waterfall, top right** — read down to find which layer pushes your threat up.
4. **Cards and chart** — which kind of wealth matters most, and whether threat is rising.
5. **What-if** — before you sell, butcher or demolish anything valuable, tick it first. Removing a pawn takes away its market value *and* the points it was worth. Prisoners count for nothing.

Examples of what it answers: 100 tiles of carpet in a mid-game colony is worth about 4.7 points, so do not demolish your floor over it. Above 1,000,000 storyteller wealth, more wealth no longer increases raids at all.

## The formula it explains

```
storyteller wealth = items + creatures + (buildings x 0.5)

base points = wealth points (curve of wealth)
            + every player pawn's points
                colonists: 15..200 each, by wealth
                animals that can learn "release": 8% of combat power
                colony mechs / subhumans: 20..40% of combat power, by wealth
                x health, x0.75 slaves, x age (Biotech), x0.3 in cryptosleep

threat points = base points x adaptation x difficulty x new colony
                -> clamped between the difficulty floor and 10,000
```

Every factor is read from the game, so on a vanilla game the breakdown reproduces the game's own number exactly.

## Settings

Open them with the **Settings** button in the panel, or *Options → Mod settings → Threat Ledger*.

| Setting | What it does |
| --- | --- |
| Animation style | 0 = off; 1 numbers roll up; 2 bars grow in; 3 wealth bars and trend line sweep in; 4 formula reveals line by line; 5 cards fade in |
| Sound style | Data terminal, hydraulics, paper ledger, threat alarm, minimal click — or sound off |
| Show sections | Wealth cards, formula waterfall, raid estimate, trend chart, warning banners, what-if simulator |
| Record threat trend | One reading per in-game hour while the tab is closed. Turn off for a strict zero cost |

## Compatibility

| Concern | How Threat Ledger handles it |
| --- | --- |
| Other mods | No Harmony patches; it only reads public game values |
| Mods that rewrite the formula | Detected and reported. The game's own value is always the headline, and the what-if simulator follows the real formula |
| DLC | Royalty, Ideology, Biotech (children, slaves, mechs), Anomaly (subhumans, pocket maps) and Odyssey use the same rules the game uses |
| Multiplayer (`rwmt.Multiplayer`) | Nothing written back, random numbers restored after every read, nothing added to the save. Tested with Multiplayer 0.11.5, host + client, panel open on both sides: no desyncs |

## Performance

- **Tab closed:** one reading per in-game hour for the trend chart (can be turned off). No tick, no game component, no patch.
- **Tab open:** about **0.24 ms per frame**, or **0.35 ms** with the what-if simulator open (measured on a 1.2M-wealth colony). The map is only scanned while the simulator is open.

## Bug reports

**https://github.com/HiDanny666/ThreatLedger/issues**

Please include your RimWorld version, your full mod list, `Player.log` (in `%USERPROFILE%\AppData\LocalLow\Ludeon Studios\RimWorld by Ludeon Studios\`), whether multiplayer was active, and what the panel showed versus what you expected. With Dev mode on, opening the tab writes a one-line `[Threat Ledger]` summary to the log — paste that line too.

## License

MIT. See [LICENSE](LICENSE).

---
---

# 威脅帳本（繁體中文）

**唯讀的 RimWorld 儀表板，讓你看清楚殖民地為什麼會遭遇這種規模的襲擊。**

RimWorld 用一條隱藏的公式決定襲擊規模，而且從不告訴你。威脅帳本新增一個分頁，把整條公式攤開，並讓你**在動手之前先試算**。

> **沒有 Harmony patch，不改動遊戲狀態，不在存檔留下任何東西。**
> 每次讀取前後都會保存並還原亂數產生器。

- **遊戲版本：** RimWorld 1.6
- **目前版本：** 0.2.0（更新內容見 [CHANGELOG.md](CHANGELOG.md)）
- **語言：** English、繁體中文、简体中文
- **前置需求：** 無（不需要 Harmony、其他模組或 DLC）
- **錯誤回報：** https://github.com/HiDanny666/ThreatLedger/issues

## 安裝

1. 到 [Releases](https://github.com/HiDanny666/ThreatLedger/releases/latest) 下載 `ThreatLedger-<版本>.zip`。
2. 解壓縮到 `RimWorld/Mods/`，得到 `RimWorld/Mods/ThreatLedger/` 資料夾。
3. 在模組清單中啟用 **Threat Ledger**，沒有排序要求。

要移除時直接刪除資料夾即可。模組不會在存檔留下任何資料，遊戲中途移除也安全。

## 如何在遊戲中取得

不需要研究、建造或製作任何東西。只要有殖民地，畫面下方就會出現「威脅帳本」分頁，就在工作／分配／健康旁邊。

## 顯示內容

| 區塊 | 內容 |
| --- | --- |
| **遊戲實際值** | 下一場襲擊真正會用的威脅點數、狀態標籤（吻合／小幅差距／其他模組改寫公式）、過去一天的變化，以及現在若發生襲擊各派系大約會來多少人 |
| **公式瀑布圖** | 財富點數、殖民者、動物、機械體加總成基礎點數，再乘上適應係數、難度與新殖民地係數，最後套用遊戲的上下限。滑鼠移到任一列可看規則 |
| **財富卡片** | 物品、生物、建築（半價計算）的市值、計入值，以及各自造成的點數 |
| **威脅趨勢** | 最多 20 個遊戲日的威脅點數變化，每遊戲小時取樣，並顯示近 1 天與近 7 天變化 |
| **模擬試算** | 點下方橫條拉起抽屜，勾選物品、建築、地板、殖民者、奴隸、動物或機械體（可篩選、搜尋），立即看到新的威脅值與襲擊人數 |
| **說明與提示** | 白話說明，以及這個殖民地的警告事項 |

## 怎麼使用

1. **左上大數字**：遊戲下一場襲擊真正會用的數值。
2. **狀態標籤**：綠色代表拆解結果與遊戲完全吻合；黃色是小幅差距（滑鼠移上看原因）；紅色代表其他模組改寫了公式，但大數字仍然正確。
3. **右上瀑布圖**：往下看，找出是哪一層把威脅推高。
4. **卡片與趨勢圖**：哪一類財富影響最大、威脅是否在上升。
5. **模擬試算**：要賣掉、宰殺或拆除貴重東西之前，先勾選試算。移除小人時會同時扣掉它的市值**和**小人點數；俘虜完全不計入。

它能回答的問題例如：中期殖民地的 100 格地毯只值約 4.7 點，不需要為此拆掉地板；故事敘述者財富超過 1,000,000 後，再增加財富也不會讓襲擊變大。

## 設定

可從面板右上角的「設定」或「選項 → 模組設定 → Threat Ledger」開啟：

| 設定 | 作用 |
| --- | --- |
| 動畫樣式 | 0 關閉；1 數字滾動遞增；2 長條逐一長出；3 財富長條與趨勢線掃入；4 公式逐行顯示；5 卡片淡入 |
| 音效樣式 | 資料終端、液壓機構、紙本帳簿、威脅警報、極簡點擊，或關閉音效 |
| 顯示區塊 | 財富卡片、公式瀑布圖、襲擊人數預估、趨勢圖、警告橫幅、模擬試算 |
| 記錄威脅趨勢 | 分頁關閉時每遊戲小時讀取一次；關閉後成本完全為零 |

## 相容性

| 項目 | 處理方式 |
| --- | --- |
| 其他模組 | 零 Harmony patch，只讀取公開的遊戲數值 |
| 改寫公式的模組 | 主動偵測並回報；主數字永遠是遊戲本身的數值，模擬試算也跟著實際公式走 |
| DLC | Royalty、Ideology、Biotech（兒童、奴隸、機械體）、Anomaly（亞人、口袋地圖）、Odyssey 皆以遊戲本身的規則計算 |
| 多人模式（`rwmt.Multiplayer`） | 不寫回任何數值、每次讀取後還原亂數、不新增存檔資料。已用 Multiplayer 0.11.5 測試（主機＋客戶端、雙方都開面板）：0 次不同步 |

## 效能

- **分頁關閉時**：只為趨勢圖每遊戲小時讀取一次（可關閉）；沒有 tick、沒有 GameComponent、沒有 patch。
- **分頁開啟時**：每幀約 **0.24 ms**，開啟模擬試算約 **0.35 ms**（120 萬財富的殖民地實測）。地圖只在模擬試算開啟時掃描。

## 錯誤回報

**https://github.com/HiDanny666/ThreatLedger/issues**

請附上遊戲版本、完整模組清單、`Player.log`（位於 `%USERPROFILE%\AppData\LocalLow\Ludeon Studios\RimWorld by Ludeon Studios\`）、是否處於多人模式，以及面板顯示的內容與你預期的差異。開啟開發者模式後打開分頁，記錄檔會出現一行 `[Threat Ledger]` 摘要，也請一併貼上。

## 授權

MIT，詳見 [LICENSE](LICENSE)。
