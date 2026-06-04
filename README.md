# 詩境｜生成式 AI 古典詩詞互動系統

版本：v1.5.0 

「詩境」是一個以古典詩詞為核心的生成式 AI 互動網站。系統結合本機唐詩資料庫與 Gemini API 流程，支援使用者透過詩名、作者、詩句片段或意境描述查詢作品，並以「詩魂現身」的方式呈現原詩、白話釋義、情緒分析、創作背景與延伸互動。


## 功能特色

- 自然語言查詩：支援作者、篇名、詩句片段與意境描述。
- 本機詩庫備援：內建 315 首唐詩資料，無 API Key 也可展示核心功能與流程。
- 詩魂現身介面：呈現篇名、作者、原詩、白話釋義、情緒與背景。
- 校注與正文分離：將「一作、又作、通」等異文註記移除。
- 輸出清理：清除原始資料中的譯文、注釋、英譯等標籤。
- 長詩直排伸縮：長篇作品仍保留直排閱讀感，並支援橫向捲動。
- 免費瀏覽器朗讀：使用 Web Speech API。
- 收藏與複製：使用 localStorage 保存收藏，並提供格式化複製。
- 雙魂對話：可選擇兩位詩人與主題，API 不可用時提供本機 fallback。
- API 狀態管理：支援 API Key 暫存、輕量測試、429 冷卻與備援提示。
- 發布驗證：提供 `scripts/release_check.js` 與 `scripts/mock_contract_check.js`。

## 檔案結構

```text
├── index.html
├── style.css
├── app.js
├── poems.json
├── scripts/
│   ├── release_check.js
│   ├── mock_contract_check.js
│   └── browser_smoke.js
├── README.md
├── USER_GUIDE.md
├── CHANGELOG.md
└── docs/
    ├── FINAL_REPORT.md
    ├── DEMO_VIDEO_SCRIPT.md
    ├── RELEASE_QA.md
    └── SOUL.md
```

## 使用方式

1. 將整個資料夾推送到 GitHub repository。
2. 在 GitHub Pages 設定中選擇部署根目錄。
3. 開啟網站後，在搜尋欄輸入詩名、作者、詩句或意境。
4. 若本機詩庫命中，系統會直接顯示詩作。
5. 若需要 AI 延伸分析，可在 API KEY 視窗輸入 Gemini API Key。

API Key 僅儲存在瀏覽器目前分頁的 `sessionStorage`。關閉分頁後 Key 會清除，專案檔案中不包含任何 API Key。

## 發布前驗證

在專案根目錄執行：

```bash
node --check app.js
node scripts/release_check.js
node scripts/mock_contract_check.js
```

目前已完成至少三輪檢討迭代與修改驗證：

1. 基準盤點與阻斷修復：確認 JS 語法、`poems.json` 解析、315 首資料與高風險掃描。
2. 功能可靠性與 Mock Gemini 驗證：補強 storage 容錯、API mock success/429/500/timeout、可及性標籤。
3. 文件與交付一致性：同步 README、使用指南、報告、影片腳本與 QA 紀錄。
4. 發布前總驗收：重跑發布檢查、產生新版 zip，確認可直接交付。

Chrome headless smoke runner 已提供於 `scripts/browser_smoke.js`。若本機 Chrome 可正常支援 `--dump-dom`，可用它做瀏覽器自動 smoke test；若 Chrome 在環境中 timeout，請以 `docs/RELEASE_QA.md` 的限制紀錄為準，並在一般瀏覽器手動開啟確認。

## 展示建議

期末展示可依序操作：

1. 搜尋 `黃鶴樓送孟浩然之廣陵`，展示本機詩庫與原詩閱讀。
2. 搜尋 `怨情`，展示輸出清理。
3. 搜尋 `琵琶行`，展示長詩直排伸縮。
4. 點擊「隨機召喚」，展示不依賴 API 的流程。
5. 展示朗讀、收藏、複製與詩藏。
6. 展示 API KEY 視窗與狀態提示。
7. 說明 Mock Gemini 驗證如何避免消耗真實配額。
