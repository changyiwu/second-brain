# 第二大腦設定指南（專案藍圖）

> 本檔為跨 Agent 通用的專案藍圖（AGENTS.md 開放標準）。任何 Agent 的每個 session 都應先讀本檔＋`handoff.md`。

## 專案簡介

維護一份不綁定特定 AI agent 的 Obsidian 第二大腦建置指南。這份文件要能被任何人、用任何 agent（Claude Code、Codex、Gemini CLI、opencode、Cursor、AntiGravity）獨立照做完成設定，因此**不依賴任何外部文件、不含跨 repo 連結**。

本專案產出的是**文件本身**，不是程式。品質標準是「拿給沒有背景知識的人，他能照著做完」。

## 關鍵時程

<!-- 目前無外部期限 -->

## 目標與路線圖

- [x] 階段一：從 codex-lazy-packs 抽離成獨立文件（移除 SKILL.md、拿掉章節編號、清除跨 repo 連結）
- [x] 階段二：改寫為通用版 v1.0（引入 `<AGENT_HOME>`／`<AGENT_RULES_FILE>` 佔位符與對照表）
- [x] 階段三：五個資料夾改用數字前綴命名，解決 Obsidian 側邊欄排序分散問題
- [x] 階段四：套用到實際 vault（`2ndbrain`），同步四個 agent 的全域設定
- [ ] 階段五：補上 agent 對照表缺漏項（AntiGravity 的規則檔名與位置尚未確認）
- [ ] 階段六：考慮是否對外發布（決定授權方式、是否附 README）

## 資料夾結構

```text
second-brain/
├── agents.md              # 本檔：專案藍圖
├── handoff.md             # 交接檔
└── 第二大腦設定指南.md    # 專案主產出（唯一交付物）
```

檔案很少是刻意的——這個專案的價值集中在單一文件，不要為了看起來像專案而增加檔案。

## 同步層級（本專案初始化至第 3 層級）

| 層級 | 平台 | 位置 | 讀取時機 |
|------|------|------|---------|
| L1 | 本地（GDrive） | `agents.md`＋`handoff.md` | 每個 session |
| L2 | GitHub | changyiwu/second-brain（私有） | 指定時 |
| L3 | Obsidian | `second-brain/專案工作流程.md` | 有需要時 |

## 相關位置

- 實際套用的 vault：`C:\Users\chang\我的雲端硬碟\2ndbrain`
- 該 vault 的筆記規則：`2ndbrain/AGENTS.md`（唯一真實來源，四個 agent 共用）
- 各 agent 全域設定：`~/.claude/CLAUDE.md`、`~/.codex/AGENTS.md`、`~/.config/opencode/opencode.json`

## 工作約定

- 任何 Agent、任何電腦：**開工先讀 `handoff.md`，收工必更新 `handoff.md`**
- 修改共用檔案前先讀最新內容，避免覆蓋其他 Agent 的變更
- 所有回應與文件使用繁體中文
- 修改前先確認計畫，優先保留原有資料結構

### 本專案特有的約定

- **不加跨 repo 連結。** 這份指南必須能獨立執行；曾因為指向 `codex-lazy-packs` 而產生死連結（見指南內「踩坑 1」）。
- **不綁定特定 agent。** 工具差異一律用佔位符＋對照表處理，不寫死某一家的路徑或功能名稱。
- **不確定的事實不要寫進對照表。** 規則檔放錯位置不會報錯、只會安靜失效，寫錯比留白更糟（見指南內「踩坑 5」）。
- 改動指南後，若涉及資料夾命名或路徑，要同步檢查實際 vault 與四個 agent 的全域設定是否需要跟著改。
