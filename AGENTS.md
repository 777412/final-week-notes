# AGENTS.md — 期末週課程筆記站（Note Hub）

> AI 開工前必讀。讀完本檔再動任何檔案。找不到答案時，以本檔為準，不要自行發明規則。

## 1. 專案目的
把我每門課的重點整理成「一個主題一頁」的靜態網站，期末週可快速複習。
目標是**可持續擴充**：之後只要說「新增一篇筆記：課程=X、主題=Y」，AI 就能照本檔做出風格一致、連結正確的新頁面。
純 HTML/CSS，無框架、無建置步驟，直接用 GitHub Pages 發佈。

## 2. 目錄結構（不得更改）
```
/
├── AGENTS.md        # 本規範
├── README.md        # 專案說明與部署步驟
├── SUBMISSION.md    # 作業繳交內容備份（不屬於網站，AI 不需修改）
├── index.html       # 首頁：所有筆記卡片 + 搜尋框
├── assets/
│   └── css/
│       └── style.css  # 全站唯一樣式檔
└── pages/           # 每篇筆記一個檔
```
- 不新增其他資料夾；圖片若有需要放 `assets/images/`（此時才建立）。
- 不引入 JS 框架、CDN、外部字型。首頁唯一的 JS 是搜尋過濾（內嵌於 index.html，< 15 行）。

## 3. 命名規則
- 筆記檔名：`pages/<課程代碼>-<主題英文kebab-case>-<兩位流水號>.html`
- 課程代碼固定：`ai`（AI 專案管理與智能代理）、`ds`（資料結構）、`mgmt`（管理學）。新課程先在本檔 §3 補一行再使用。
- 流水號為全站遞增（不是每課各自重算）：**先查看 `pages/` 內現有最大編號，再加 1**，不要依賴本檔或舊範例中的數字。
- 範例：`pages/ai-agent-patterns-01.html`

## 4. 視覺規範（全部寫在 assets/css/style.css 的 :root，不可在 HTML 內寫 inline style）
| 變數 | 色碼 | 用途 |
|---|---|---|
| `--paper` | `#F2F5F3` | 頁面背景 |
| `--ink` | `#16262B` | 文字、標題 |
| `--line` | `#C9D4CF` | 邊框、分隔線 |
| `--accent` | `#1F5EFF` | 連結、重點邊線 |
| `--mark` | `#FFE45C` | 螢光筆重點（`<mark>`） |
- 字型：`'Noto Sans TC','PingFang TC',sans-serif`；程式碼 `ui-monospace,monospace`。
- 重點句一律用 `<mark>` 包起來，每篇 2~4 處，不得整段標螢光。
- 手機優先；寬度 ≤ 640px 時卡片單欄。

## 5. 筆記頁固定結構（依序，缺一不可）
1. `<header>`：`<a href="../index.html">返回首頁</a>`
2. `<h1>` 主題名稱 + `<p class="meta">` 內含課程標籤 `<span class="tag tag-ai|tag-ds|tag-mgmt">`
3. `<section class="summary">`：**一句話總結**（≤ 60 字）
4. 2~4 個 `<section>`，各有 `<h2>`：概念說明 / 步驟或比較表 / 範例
5. `<section class="review">`：**自我檢查**，3 題問答（`<details><summary>題目</summary>答案</details>`）
6. `<footer>`：最後更新日期（格式 `YYYY-MM-DD`）
- `<head>` 必須有：`lang="zh-Hant"`、`charset`、`viewport`、`<title>主題 - 筆記站</title>`、`<link rel="stylesheet" href="../assets/css/style.css">`
- 內文只放我學過的內容；**不確定的事實標註「待查證」**，不得編造書名、頁碼、公式。

## 6. 新增筆記的 SOP（AI 必須依序執行）
1. 讀取本檔與 `assets/css/style.css`，不重造樣式；並查看 `pages/` 內現有最大流水號。
2. 依 §3 決定檔名（最大號 + 1），在 `pages/` 建立新頁，套用 §5 結構。
3. 開啟 `index.html`，在註解 `<!-- NOTES:START -->` 的**下一行**插入新卡片（最新在最上）：
```html
<li class="card" data-course="ds"><a href="pages/ds-xxx-NN.html"><span class="tag tag-ds">資料結構</span><h2>主題名稱</h2><p>一句話總結</p></a></li>
```
4. 更新 `index.html` 內 `<span id="count">` 的筆記總數。
5. 驗收清單（逐項自查並在回覆中列出結果）：
   - [ ] 新頁能從首頁點進去，且能點回首頁（相對路徑：首頁用 `pages/…`，子頁用 `../…`）
   - [ ] 全站沒有死連結、沒有 inline style
   - [ ] 標籤 class 與課程代碼一致
   - [ ] 有 2~4 處 `<mark>`、3 題自我檢查
   - [ ] 流水號沒有重複，且等於原最大號 + 1

## 7. 禁止事項
- 不得刪除或改寫既有筆記內容，除非我明確要求。
- 不得改動色碼、目錄結構、命名規則；若覺得需要改，先提出建議等我同意。
- 不得加入追蹤碼、廣告、外部資源。

## 8. 範例指令（我之後會這樣下指令）
> 請讀 AGENTS.md，新增一篇筆記：課程=mgmt，主題=管理者的三種技能。
