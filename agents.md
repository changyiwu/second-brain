# 第二大腦設定指南（專案藍圖）

> 本檔為跨 Agent 通用的專案藍圖（AGENTS.md 開放標準）。任何 Agent 的每個 session 都應先讀本檔＋`handoff.md`。

## 專案簡介

維護一份不綁定特定 AI agent 的 Obsidian 第二大腦建置指南。這份文件要能被任何人、用任何 agent（Claude Code、Codex、opencode、Antigravity）獨立照做完成設定，因此**不依賴任何外部文件、不含跨 repo 連結**。

本專案產出的是**文件本身**，不是程式。品質標準是「拿給沒有背景知識的人，他能照著做完」。

## 關鍵時程

<!-- 目前無外部期限 -->

## 目標與路線圖

- [x] 階段一：從 codex-lazy-packs 抽離成獨立文件（移除 SKILL.md、拿掉章節編號、清除跨 repo 連結）
- [x] 階段二：改寫為通用版 v1.0（引入 `<AGENT_HOME>`／`<AGENT_RULES_FILE>` 佔位符與對照表）
- [x] 階段三：五個資料夾改用數字前綴命名，解決 Obsidian 側邊欄排序分散問題
- [x] 階段四：套用到實際 vault（`2ndbrain`），同步四個 agent 的全域設定
- [x] 階段五：補上「橋接檔」缺口（vault 與全域各補一份 `CLAUDE.md`，指南新增 3-3、踩坑 7 與對應驗證項）
- [x] 階段六：收斂 agent 對照表為四家（移除 Gemini CLI 與 Cursor，查證 opencode 與 Antigravity 2.0 的規則檔），並補齊本機缺的兩份全域規則檔
- [ ] 階段七：考慮把「設定檔 ≠ 規則檔」寫成指南的踩坑 8（`opencode.json` 存在讓缺口看起來像已完成）
- [ ] 階段八：考慮是否對外發布（決定授權方式、是否附 README）

## 資料夾結構

```text
second-brain/
├── agents.md              # 本檔：專案藍圖
├── CLAUDE.md              # 橋接檔：@agents.md，供只讀 CLAUDE.md 的 Claude Code 使用
├── handoff.md             # 交接檔
└── 第二大腦設定指南.md    # 專案主產出（唯一交付物）
```

檔案很少是刻意的——這個專案的價值集中在單一文件，不要為了看起來像專案而增加檔案。

## 同步層級（本專案初始化至第 3 層級）

| 層級 | 平台 | 位置 | 讀取時機 |
|------|------|------|---------|
| L1 | 本地（GDrive） | `agents.md`＋`handoff.md` | 每個 session |
| L2 | GitHub | changyiwu/second-brain（**公開**） | 指定時 |
| L3 | Obsidian | `second-brain/專案工作流程.md` | 有需要時 |

## 相關位置

- 實際套用的 vault：`C:\Users\chang\我的雲端硬碟\2ndbrain`
- 該 vault 的筆記規則：`2ndbrain/AGENTS.md`（唯一真實來源，四個 agent 共用）
- 該 vault 的橋接檔：`2ndbrain/CLAUDE.md`（`@AGENTS.md` import，不放規則內容）
- 各 agent 全域規則檔：`~/.claude/CLAUDE.md`、`~/.codex/AGENTS.md`、`~/.config/opencode/AGENTS.md`、`~/.gemini/GEMINI.md`（Antigravity）
- `~/.config/opencode/opencode.json` 管的是 MCP、provider 與權限，不是規則檔，兩者不要混為一談

## 三個檔案的職責（依「時效性」分家，不是依「詳細程度」）

| 檔案 | 時效 | 寫入方式 | 放什麼 |
|------|------|---------|--------|
| `handoff.md` | **只對下一個 session 有效**，過期即丟 | 每次收工整份重寫 | 做到哪、下一步、**這次**的暫時 workaround |
| `agents.md`（本檔） | **長期有效**，每個 session 都適用 | 只有規則本身變了才改 | 目標、路線圖、常設規則、結構 |
| Obsidian／`git log` | **歷史**：發生過什麼、為什麼 | 只增不刪 | 決策紀錄、踩坑完整版、逐次進度 |

驗收標準：**`handoff.md` 整份刪掉，不應損失任何長期資訊**——會的話代表該升級進本檔卻沒升級。

**本檔不要出現的東西**：❌ `## 最近進度`／逐次工作紀錄、❌ 決策理由與踩坑完整版。歷史寫 L3 筆記的〈🗓️ 最近更動紀錄〉〈🧠 決策紀錄〉〈🕳️ 踩坑筆記〉；踩過的坑只把**結論**收斂成一條祈使句寫進〈工作約定〉，原因留 L3。

## 專案專屬規則（補充）

- **設定檔存在會讓規則檔的缺口看起來像已完成**。opencode 的 `opencode.json` 把 MCP、provider、權限都設好了，看起來很完整，但**它不是規則檔**——opencode 的全域規則要另開 `~/.config/opencode/AGENTS.md`。藍圖曾把 `opencode.json` 列為「全域設定」，缺口因此躲了很久
- **Antigravity 的家目錄是 `~/.gemini/`，不是 `~/.antigravity/`**（後者不存在）。它自 v1.20.5 起同時讀 `AGENTS.md` 與 `GEMINI.md`，所以 vault 端**不需要**替它做橋接檔
- **vault 的筆記規則只維護 `2ndbrain/AGENTS.md` 一份**，各 agent 全域檔只記路徑、不重複定義規則；`2ndbrain/CLAUDE.md` 是橋接檔，只有 `@AGENTS.md`，**不要往裡面補規則內容**
- **`2ndbrain` 內五處提到舊資料夾名的地方是歷史紀錄**（W29 週報、四份專案工作流程），刻意不改，**不要「順手修正」**
- 對照表的四家都是查證過的（opencode 與 Antigravity 的欄位來自官方文件與 changelog，不是本機實測或推測）。新增任何一家前先查文件，不確定就留在「其他：查該工具文件」

## 工作約定

- 任何 Agent、任何電腦：**開工先讀 `handoff.md`，收工必更新 `handoff.md`**
- 修改共用檔案前先讀最新內容，避免覆蓋其他 Agent 的變更
- 所有回應與文件使用繁體中文
- 修改前先確認計畫，優先保留原有資料結構

### 本專案特有的約定

- **repo 是公開的。** 任何寫進 commit 的內容都是對外發布。不要放個人資料、實際檔案路徑以外的隱私資訊、或任何憑證。
- **git 作者 email 固定用 `changyiwu@users.noreply.github.com`**（已設定在本專案的 local config），不要用真實 email。

- **不加跨 repo 連結。** 這份指南必須能獨立執行；曾因為指向 `codex-lazy-packs` 而產生死連結（見指南內「踩坑 1」）。
- **不綁定特定 agent。** 工具差異一律用佔位符＋對照表處理，不寫死某一家的路徑或功能名稱。
- **不確定的事實不要寫進對照表。** 規則檔放錯位置不會報錯、只會安靜失效，寫錯比留白更糟（見指南內「踩坑 5」）。
- **規則只維護一份，其他檔名一律做橋接檔。** 橋接檔只放 import／指路，不複製規則內容，否則兩份必然分叉（見指南內「踩坑 6、7」）。
- **檔案類的交接紀錄，寫之前先實際列一次目錄。** 寫「已建立」但檔案不存在，已發生過一次（`~/.claude/CLAUDE.md`）。
- 改動指南後，若涉及資料夾命名或路徑，要同步檢查實際 vault 與四個 agent 的全域設定是否需要跟著改。
