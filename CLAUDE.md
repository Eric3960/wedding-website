# 婚禮網站 — 專案說明（給 AI 助手的交接文件）

昱恩（Yu-En，新郎，就是使用者本人 Eric）＆ 雨蕎（Yu-Chiao，新娘）的婚禮網站。
婚期：2027-05-23（日）高雄。典禮 9:30 真耶穌教會十全教會；婚宴 13:00 老新台菜十全店。

## 架構

純靜態 HTML/CSS/JS，**無框架、無建置流程**，多頁式（仿 shetoshi.minted.us）：

- `index.html` — 首頁：滿版 hero（倒數計時）→ 我們的故事 → RSVP（點戒指照 `images/rsvp.jpg` 開啟 en-vite-app.com 表單，連結寫在 index.html）
- `gallery.html` / `events.html` / `parking.html` / `faq.html` — 選單各自獨立頁
- `style.css` — 共用樣式；配色全部走 `:root` CSS 變數
- `script.js` — 共用：中英 i18n 字典、語言切換（localStorage `wedding-lang`）、倒數、手機選單、相簿燈箱、目前頁 nav 標示
- `images/` — 照片；`首頁.jpg` 是 hero 背景（已裁掉手機截圖黑邊）
- 專案根目錄的 `首頁.jpg`、`參考圖.jpg` 是使用者放的原始檔，不要刪

## 鐵則

1. **所有看得見的文字都要雙語**：頁面元素掛 `data-i18n="key"`，文字內容同步寫進 `script.js` 的 `I18N.zh` 和 `I18N.en` 兩個字典。只改 HTML 不改字典的話，切換語言會跳回舊字。
2. **導覽列改動要同步到全部 5 個 HTML**（nav 是複製貼上的，沒有共用模板）。
3. 選單只有五項：首頁、甜蜜相簿、活動流程、停車資訊、常見問題（使用者指定，勿加）。

## 風格

睡美人溫柔粉：蜜糖粉/淡粉/銀霧白/粉 Topaz 金（`--deep #66293d`、`--navy`、`--dusty`、`--baby`、`--ice`、`--silver`、`--gold`）。
前一版是仙度瑞拉夢幻藍（git 歷史 commit `768aff8` 以前），使用者在比較兩種風格，可能會要求切回或調整。
Hero 文字有白色光暈 + 加強版白霧漸層，是為了寬螢幕可讀性（使用者反映過字看不清楚）。

## 部署

GitHub Pages：repo `Eric3960/wedding-website`（public），網址 https://eric3960.github.io/wedding-website/
更新方式：commit 後 `git push` 即自動部署（約 1 分鐘生效）。Git 認證走 Git Credential Manager，已設定好。
注意：`gh` CLI 有免安裝版在 `%LOCALAPPDATA%\gh-cli\bin\gh.exe` 但**未登入**（device flow 一直超時）；要呼叫 GitHub API 可用 `git credential fill` 拿 token。

## 本地驗證技巧

headless Edge 截圖：`msedge --headless=new --user-data-dir=<臨時資料夾> --window-size=1280,950 --virtual-time-budget=12000 --screenshot=out.png <file:// URL>`（中文路徑要 URL encode）。
整頁長截圖會被 hero 的 100svh 撐爆：先複製一份 `_preview.html` 加 `<style>html{scroll-behavior:auto!important}.hero{min-height:900px!important}</style>` 再截，截完刪掉。

## 待辦（等使用者提供）

- [ ] 婚紗照拍完後更換 `gallery.html` 的照片（目前是生活照）
- [ ] 「我們的故事」目前是**草稿**，使用者會給最終版
- [ ] 停車資訊兩個會場都還是「整理中」占位文字
- [ ] 雨蕎的英文拼法暫用 Yu-Chiao，護照拼法不同的話要改（`script.js` 的 `hero.bride`）
