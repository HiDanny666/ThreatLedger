# Threat Ledger

**A read-only RimWorld dashboard that shows exactly why your colony gets the raids it gets.**

RimWorld decides raid size with a hidden formula and never tells you any of it.
Threat Ledger adds one tab that lays the whole thing open — and lets you test a change before you commit to it.

> **No Harmony patches. No game state changes. Nothing in your save.**
> The random number generator is saved and restored around every read.

- **Game version:** RimWorld 1.6 / 1.7
- **Current version:** 0.3.1 — see [What's new](#whats-new-in-031) and [CHANGELOG.md](CHANGELOG.md)
- **Languages:** English, 繁體中文, 简体中文
- **Requires:** nothing (no Harmony, no other mods, no DLC)
- **Bug reports:** https://github.com/HiDanny666/ThreatLedger/issues

---

## What's new in 0.3.1

- **RimWorld Together support** ([Workshop 3005289691](https://steamcommunity.com/sharedfiles/filedetails/?id=3005289691)) — the trade threat panel now also opens beside RimWorld Together's **transfer window** (rows set to "Offer" leave with their whole stack; a pawn leaves with everything they wear and carry, and their pawn points) and beside **transfer requests** from other players (what you would receive, on the home map or in your caravan). While you answer a trade request from your settlement it shows the whole exchange. RimWorld Together is not lockstep and Threat Ledger only reads, so nothing it syncs is touched.
- **Fixed:** mods installed from the Workshop and listed with the `_steam` suffix (when a local copy with the same id exists) are now detected — RimWorld Together and Multiplayer.
- Long names in the trade panel are shortened instead of wrapping onto the next row (hover for the full name).
- Tested in game with RimWorld Together on its real transfer windows: 29/29 checks; 161 unit tests.

## What's new in 0.3.0

- **Trade threat impact panel** — opens by itself beside every trade window (caravans, orbital traders, settlements; also Multiplayer's trade window). As you change counts it shows the threat after the deal, wealth gained / lost, pawns joining / leaving, and for **each bought or sold row** its wealth change and how many points it adds or removes (hover for the per-unit effect). Silver paid or received is its own row.
- **Add-items simulation** — "+ Add" in the what-if drawer: search any item or buildable building, set count, material and quality, and see how much bigger the next raid gets. Combines with ticked removals.
- **Crop harvest estimate** — "Harvest: ready now" / "Harvest: all grown" add your crops as the produce they would give.
- **Multiplayer Multifaction fix** — another player faction's colony is now priced with that faction's own storyteller, difficulty, adaptation and pawns.
- Tested with Multiplayer 0.11.5 + MP Desync Fixes 0.3.3 (host + arbiter at top speed, no desync) and with Combat Extended.

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
| **+ Add** | In the simulator: add any item or buildable building (count, material, quality) or your crops' harvest, and see the threat it adds |
| **Trade threat impact** | Beside every trade window: the threat after the deal and the effect of each buy and sell row |
| **Help & notes** | Plain-language explanation and any warnings about this colony |

## How to use it

1. **Big number, top left** — what the game will really use for the next raid.
2. **Status badge** — green means Threat Ledger's breakdown matches the game exactly. Amber is a small gap (hover for why). Red means another mod changed the formula; the big number is still correct.
3. **Waterfall, top right** — read down to find which layer pushes your threat up.
4. **Cards and chart** — which kind of wealth matters most, and whether threat is rising.
5. **What-if** — before you sell, butcher or demolish anything valuable, tick it first. Removing a pawn takes away its market value *and* the points it was worth. Prisoners count for nothing.

6. **+ Add** — before you buy, craft or build something valuable, add it: pick it, choose material and quality, type the count. Items count in full; buildings as installed, at half value.
7. **Trading** — just open the trade. The panel beside it shows row by row what each purchase or sale does to the next raid. Bought colonists and slaves add pawn points and bring their gear; a sold colonist leaves their weapon and inventory behind. Close it with its X if you do not need it.

Examples of what it answers: 100 tiles of carpet in a mid-game colony is worth about 4.7 points, so do not demolish your floor over it. Above 1,000,000 storyteller wealth, more wealth no longer increases raids at all.

### How crops count

Plants growing on the map — your crops and trees alike — are **not wealth at all**: the game only counts haulable items, your buildings and floors, and your pawns. A hydroponics basin or plant pot counts as a building; a crop only counts once harvested, as produce at full item value. A field of ripe rice does not attract raids; the rice in your freezer does. The harvest buttons in "+ Add" show how much a harvest will add (average yield, with the difficulty's crop yield and plant damage).

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
| Show the trade threat impact panel | Opens the panel beside every trade window; it only computes while a trade is open |

## Compatibility

| Concern | How Threat Ledger handles it |
| --- | --- |
| Other mods | No Harmony patches; it only reads public game values |
| Mods that rewrite the formula | Detected and reported. The game's own value is always the headline, and the what-if simulator follows the real formula |
| DLC | Royalty, Ideology, Biotech (children, slaves, mechs), Anomaly (subhumans, pocket maps) and Odyssey use the same rules the game uses |
| Multiplayer (`rwmt.Multiplayer`) | Nothing written back, random numbers restored after every read, nothing added to the save; the panel, simulator and trade panel are client-local. With Multifaction, another player faction's colony is read as that faction. Tested with Multiplayer 0.11.5: host + arbiter at top speed for 50,754 ticks with the panel open, no desync |
| MP Desync Fixes 0.3.3 | Compatible, tested together with Multifaction and async time |
| Combat Extended | Compatible, tested |
| RimWorld Together | Supported, tested. Not lockstep and Threat Ledger only reads, so nothing it syncs is touched. The trade panel also opens beside its transfer window and transfer requests (whole stacks; a pawn leaves with all their gear) |

## Performance

- **Tab closed:** one reading per in-game hour for the trend chart (can be turned off). No tick, no game component, no patch.
- **Tab open:** about **0.24 ms per frame**, or **0.35 ms** with the what-if simulator open (measured on a 1.2M-wealth colony). The map is only scanned while the simulator is open.
- **Trade panel:** 0.04 µs per frame while no trade is open; while trading the deal is re-read twice a second (6-15 µs each).

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

- **遊戲版本：** RimWorld 1.6 / 1.7
- **目前版本：** 0.3.1（更新內容見下方「0.3.1 更新內容」與 [CHANGELOG.md](CHANGELOG.md)）
- **語言：** English、繁體中文、简体中文
- **前置需求：** 無（不需要 Harmony、其他模組或 DLC）
- **錯誤回報：** https://github.com/HiDanny666/ThreatLedger/issues

## 0.3.1 更新內容

- **支援 RimWorld Together**（[Workshop 3005289691](https://steamcommunity.com/sharedfiles/filedetails/?id=3005289691)）：交易威脅影響面板現在也會出現在 RimWorld Together 的**轉移視窗**旁（設為「Offer」的列整疊離開；送出的角色帶走全身穿戴與攜帶的東西，以及角色點數），以及其他玩家送來的**轉移請求**旁（你會收到什麼，放到家園地圖或你的商隊）。從據點回覆交易請求時，會列出整筆交換。RimWorld Together 不是鎖步同步，威脅帳本又只讀取，不會碰到它同步的任何東西。
- **修正**：從 Workshop 安裝、模組清單中帶 `_steam` 後綴的模組（同 ID 另有本機副本時）現在也偵測得到——RimWorld Together 與 Multiplayer 皆是。
- 交易面板中過長的名稱改為截斷，不再換行壓到下一列（滑鼠移上去可看全名）。
- 已載入 RimWorld Together 以它真實的轉移視窗在遊戲中實測：29/29 項；單元測試 161 項。

## 0.3.0 更新內容

- **交易威脅影響面板**：每次開啟交易視窗（商隊、軌道商船、據點；多人連線的交易視窗也可以）都會自動出現在旁邊。調整數量時即時顯示交易後的威脅點數、財富增減、小人加入／離開，以及**每一筆買入、賣出**的財富變化與點數增減（滑鼠移上去看平均每 1 個的影響）。付出或收到的白銀獨立一列。
- **新增物品試算**：模擬試算抽屜的「＋新增」，搜尋任何物品或可建造建築，設定數量、材質、品質，看下一場襲擊會變大多少；可和勾選的移除項目合併計算。
- **作物收成預估**：「收成：現在可收」「收成：全部成熟」把作物換算成收成後的農產品。
- **多人連線「多陣營」修正**：查看別的玩家陣營殖民地時，改用該陣營自己的說書人、難度、適應係數與小人計算。
- 已與 Multiplayer 0.11.5 + MP Desync Fixes 0.3.3（主機＋仲裁者最快速度，0 次不同步）及 Combat Extended 一起實測。

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
| **＋新增** | 在模擬試算裡加入任何物品或可建造建築（數量、材質、品質），或作物的收成，看會增加多少威脅 |
| **交易威脅影響** | 每個交易視窗旁邊：交易後的威脅點數，以及每一筆買賣的影響 |
| **說明與提示** | 白話說明，以及這個殖民地的警告事項 |

## 怎麼使用

1. **左上大數字**：遊戲下一場襲擊真正會用的數值。
2. **狀態標籤**：綠色代表拆解結果與遊戲完全吻合；黃色是小幅差距（滑鼠移上看原因）；紅色代表其他模組改寫了公式，但大數字仍然正確。
3. **右上瀑布圖**：往下看，找出是哪一層把威脅推高。
4. **卡片與趨勢圖**：哪一類財富影響最大、威脅是否在上升。
5. **模擬試算**：要賣掉、宰殺或拆除貴重東西之前，先勾選試算。移除小人時會同時扣掉它的市值**和**小人點數；俘虜完全不計入。

6. **＋新增**：要購買、製作或建造貴重東西之前，先加入試算：選物品、材質、品質，輸入數量。物品全額計入；建築以安裝後半價計算。
7. **交易時**：直接開交易視窗，旁邊的面板會逐列顯示每一筆買賣對下一場襲擊的影響。買來的殖民者或奴隸會增加小人點數並帶來裝備；賣掉殖民者時武器和背包會留下。用不到可以按 X 關閉。

它能回答的問題例如：中期殖民地的 100 格地毯只值約 4.7 點，不需要為此拆掉地板；故事敘述者財富超過 1,000,000 後，再增加財富也不會讓襲擊變大。

### 作物怎麼算

地圖上正在生長的植物（包括你種的作物和樹）**完全不算財富**：遊戲只計算可搬運的物品、你擁有的建築與地板、你的小人。水耕盆、花盆本身算建築；作物收成變成農產品後，才以物品全額計入。一整片成熟稻田不會吸引襲擊，冷凍庫裡的稻米才會。「＋新增」的收成按鈕可以看收成後會增加多少（平均產量，套用難度作物產量係數與植株受損程度）。

## 設定

可從面板右上角的「設定」或「選項 → 模組設定 → Threat Ledger」開啟：

| 設定 | 作用 |
| --- | --- |
| 動畫樣式 | 0 關閉；1 數字滾動遞增；2 長條逐一長出；3 財富長條與趨勢線掃入；4 公式逐行顯示；5 卡片淡入 |
| 音效樣式 | 資料終端、液壓機構、紙本帳簿、威脅警報、極簡點擊，或關閉音效 |
| 顯示區塊 | 財富卡片、公式瀑布圖、襲擊人數預估、趨勢圖、警告橫幅、模擬試算 |
| 記錄威脅趨勢 | 分頁關閉時每遊戲小時讀取一次；關閉後成本完全為零 |
| 交易時顯示交易威脅影響面板 | 在每個交易視窗旁邊顯示面板；只在交易視窗開著時計算 |

## 相容性

| 項目 | 處理方式 |
| --- | --- |
| 其他模組 | 零 Harmony patch，只讀取公開的遊戲數值 |
| 改寫公式的模組 | 主動偵測並回報；主數字永遠是遊戲本身的數值，模擬試算也跟著實際公式走 |
| DLC | Royalty、Ideology、Biotech（兒童、奴隸、機械體）、Anomaly（亞人、口袋地圖）、Odyssey 皆以遊戲本身的規則計算 |
| 多人模式（`rwmt.Multiplayer`） | 不寫回任何數值、每次讀取後還原亂數、不新增存檔資料；面板、試算與交易面板都只在本機。開「多陣營」時，別的玩家陣營殖民地以該陣營身分讀取。已用 Multiplayer 0.11.5 測試：主機＋仲裁者最快速度 50,754 tick、開著面板，0 次不同步 |
| MP Desync Fixes 0.3.3 | 相容，已在多陣營＋非同步時間下一起實測 |
| Combat Extended | 相容，已實測 |
| RimWorld Together | 支援，已實測。它不是鎖步同步、威脅帳本又只讀取，不會碰到它同步的東西。交易面板也會出現在它的轉移視窗與轉移請求旁（一律整疊；送出的角色帶走全身裝備） |

## 效能

- **分頁關閉時**：只為趨勢圖每遊戲小時讀取一次（可關閉）；沒有 tick、沒有 GameComponent、沒有 patch。
- **分頁開啟時**：每幀約 **0.24 ms**，開啟模擬試算約 **0.35 ms**（120 萬財富的殖民地實測）。地圖只在模擬試算開啟時掃描。
- **交易面板**：沒有交易時每幀 0.04 µs；交易中每秒讀取交易 2 次（每次 6～15 µs）。

## 錯誤回報

**https://github.com/HiDanny666/ThreatLedger/issues**

請附上遊戲版本、完整模組清單、`Player.log`（位於 `%USERPROFILE%\AppData\LocalLow\Ludeon Studios\RimWorld by Ludeon Studios\`）、是否處於多人模式，以及面板顯示的內容與你預期的差異。開啟開發者模式後打開分頁，記錄檔會出現一行 `[Threat Ledger]` 摘要，也請一併貼上。

## 授權

MIT，詳見 [LICENSE](LICENSE)。
