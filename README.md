# 詩境｜生成式 AI 古典詩詞互動系統

「詩境」是一個純靜態網頁作品，結合本機唐詩資料庫與 Gemini API，讓使用者用作者、篇名、詩句片段或意境描述召喚詩作，並以「詩魂現身」的方式閱讀古典詩詞。

## 線上展示

部署到 GitHub Pages 後，網址通常會是：

```text
https://paul931130.github.io/-shijing/
```

如果 repository 名稱不同，請將網址最後的 `-shijing` 改成實際 repo 名稱。

## 第二階段改版重點

| 類別 | 說明 |
|---|---|
| UI 修正 | 移除重複的「詩藏」按鈕，保留主分頁中的詩藏入口與收藏數量 badge。 |
| 隨機召喚 | 新增「🎲 隨機一首」，直接從本機 `poems.json` 抽詩，不消耗 Gemini API。 |
| 免費朗讀 | 新增瀏覽器內建朗讀功能，使用 `speechSynthesis`，不需要 ElevenLabs 或任何語音 API key。 |
| 文件更新 | 同步更新 README、USER_GUIDE、PROJECT_REPORT，並新增 DEMO_SCRIPT。 |

## 專案特色

- 本機 `poems.json` 優先查詢，減少 API 消耗。
- 「🎲 隨機一首」可從本機詩庫快速召喚作品。
- 詩作原文與詩魂自語支援免費瀏覽器朗讀。
- Gemini API 可補足意境式查詢與詩魂問答。
- API Key 只存 `sessionStorage`，關閉分頁後清除。
- 貼上 Gemini API Key 後會延遲自動輕量測試一次；同一把 key 不重複測，遇到 `Too many requests / 429` 會暫停自動測試 60 秒。
- 明確顯示來源：Gemini 或本機詩庫。
- API 狀態條顯示已連線、僅本機或配額受限。
- 錯誤卡提供重試 API、切換 API Key、推薦本機類似文章。
- 支援收藏詩作與複製詩作。
- CSS/JS 已拆分，適合 GitHub Pages 靜態部署。

## 檔案結構

```text
-shijing/
├── index.html              # 網站入口
├── style.css               # 介面樣式
├── app.js                  # 互動、本機詩庫、TTS 與 API 邏輯
├── poems.json              # 本機詩詞資料
├── README.md               # 專案說明
├── CHECK.txt               # 發布檔案 SHA-256
├── USER_GUIDE.md           # 使用者指南
├── PROJECT_REPORT.md       # 專題報告 Markdown
├── DEMO_SCRIPT.md          # 影片展示腳本
└── docs/
    ├── README.md
    ├── USER_GUIDE.md
    ├── PROJECT_REPORT.md
    ├── DEMO_SCRIPT.md
    └── SOUL.md
```

## 使用方式

1. 開啟網站。
2. 可先不輸入 API Key，直接查詢本機詩庫，例如：`靜夜思`、`石壕吏`、`床前明月光`。
3. 可按「🎲 隨機一首」從本機詩庫抽出作品，不消耗 Gemini API。
4. 查到詩後，可按「朗讀」使用瀏覽器內建語音朗讀詩文或詩魂自語。
5. 若要使用 Gemini，點左側 `API KEY`，貼上 key 後會自動輕量測試一次；測試成功後即可使用 AI 分析與詩魂問答。
6. 查到詩後可切換分析頁籤、向詩魂提問、收藏或複製詩作。
7. 可到「雙魂對話」選兩位詩人，輸入主題後生成對話。

## 本機詩庫限制

目前 `poems.json` 主要收錄唐詩。本機模式不一定能查到宋詞或其他朝代作品，例如蘇軾、李清照的部分作品可能需要 Gemini API 才能生成解讀。

## 免費瀏覽器朗讀

本專案使用瀏覽器內建 Web Speech API 的 `speechSynthesis` 進行朗讀。這項功能不需要 ElevenLabs、不需要後端，也不消耗 API 額度。

注意：朗讀音色會依瀏覽器與作業系統而不同。建議使用 Chrome 或 Edge 測試，並確認系統音量與中文語音可用。

## API Key 安全

本專案不會把 API Key 寫進程式碼，也不會保存到長期 `localStorage`。Key 只暫存在目前分頁的 `sessionStorage`，關閉分頁後即清除。

注意：這仍是前端直連 API 的展示型做法，適合課程展示與個人使用。若要公開給大量使用者，建議改成後端代理服務，避免 key 暴露與配額濫用。

## 本機測試

不要直接雙擊 `index.html`，因為 `fetch("poems.json")` 在 `file://` 模式下可能失敗。請在專案資料夾執行：

```bash
python -m http.server 8000
```

或 Windows：

```bash
py -m http.server 8000
```

然後開啟：

```text
http://localhost:8000/
```

建議測試：

- `靜夜思`
- `石壕吏`
- `床前明月光`
- `🎲 隨機一首`
- 不輸入 API key 直接按「朗讀」

## 發布到 GitHub Pages

1. 建立 GitHub repository。
2. 上傳本資料夾所有檔案。
3. 確認 `poems.json` 與 `index.html` 在同一層。
4. 到 repository 的 Settings → Pages。
5. Source 選 `Deploy from a branch`。
6. Branch 選 `main`，資料夾選 `/root`。
7. 等待 GitHub 產生公開網址。

## 技術架構

- HTML：頁面結構
- CSS：古典紙本視覺、直排詩文、響應式版面
- JavaScript：本機詩庫查詢、隨機召喚、瀏覽器 TTS、Gemini API、收藏、互動狀態
- Gemini 2.5 Flash：意境式查詢、詩魂問答、雙魂對話
- Web Speech API：免費瀏覽器朗讀
- GitHub Pages：靜態網站部署

## 測試檢查

- `node --check app.js`
- 確認 `index.html` 不含硬編碼 API Key
- 確認 `poems.json` 可解析且筆數約 315
- 確認只剩一個「詩藏」入口
- 確認「🎲 隨機一首」不需要 Gemini key
- 確認不填語音 API key 也能使用瀏覽器朗讀


## G2 修正版重點

- 修正原文白色方框：依詩句長度自動調整高度，短詩不再硬撐，文字置中。
- 修正隨機召喚：隨機詩來源為本機詩庫，但不再覆蓋 Gemini API 連線狀態。
- 修正本機相近推薦：使用本機資料時不再誤顯示 API 未連線。
- 優化手機版導覽列與操作按鈕，降低擋到標題或擠壓內容的機率。
- 啟動時若本分頁已有暫存 API key，先維持已連線狀態，再背景輕量測試。
