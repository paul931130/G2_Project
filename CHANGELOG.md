# CHANGELOG｜詩境版本紀錄

## v1.5.0｜release-ready 發布整理

本版本目標是讓專案可直接發布到 GitHub Pages，並可直接作為期末專題交付。除了程式碼，也同步更新 README、USER_GUIDE、FINAL_REPORT、DEMO_VIDEO_SCRIPT、RELEASE_QA 與外層 DOCX 文件。

### 穩定性

- 新增 storage 容錯：sessionStorage/localStorage 不可用時不再使頁面初始化失敗。
- 收藏與字級設定改用安全讀寫，壞掉的 localStorage 內容會 fallback。
- 本機詩庫載入與隨機召喚提示更清楚。
- 保留本機詩庫優先查詢，避免無 key 展示中斷。

### Mock Gemini 與發布驗證

- 新增 localhost-only Mock Gemini 測試入口。
- 支援 mock success、429、500、timeout。
- 新增 `scripts/release_check.js` 檢查語法、資料、風險掃描、版本與文件 marker。
- 新增 `scripts/mock_contract_check.js` 驗證不呼叫真實 Gemini 的 API 流程。
- 新增 `scripts/browser_smoke.js` 作為 headless Chrome smoke runner。

### 可及性與發布

- 導覽列新增 `role="tablist"`、`role="tab"`、`aria-selected` 與 `aria-controls`。
- 主要輸入、API Key 欄位與動態聊天輸入補上 accessible name。
- 新增 `.sr-only` 工具 class。
- cache busting 更新為 `20260604-v150-release-ready`。

### 文件

- README 更新為 GitHub Pages / 期末交付導向。
- USER_GUIDE 更新操作流程、API 狀態與 Mock Gemini 說明。
- FINAL_REPORT 補入 v1.5.0、三輪以上檢討迭代、發布驗證與反思。
- DEMO_VIDEO_SCRIPT 更新解說影片腳本與現場展示話術。
- RELEASE_QA 記錄四輪驗證結果與 Chrome headless timeout 限制。

## v1.4.1｜期末展示修正

- 清理詩庫輸出標籤。
- 分離長序文與校注。
- 放大閱讀字級。
- 改善長詩直排白框伸縮。
- 正式化期末展示文件。

## v1.4.0｜校注分離

- 將異文註記從原詩正文分離。
- 修正快取問題。
- 強化長詩閱讀穩定性。

## v1.3.0｜穩定化

- 強化 API Key、安全性、狀態列、錯誤處理與手機版。

## v1.2.0｜功能擴充

- 新增隨機召喚、收藏、複製、朗讀、詩魂問答與雙魂對話。

## v1.1.0｜結構拆分

- 拆分 HTML、CSS、JS 與 poems.json。

## v1.0.0｜初版概念

- 建立 AI 查詩與詩魂呈現雛形。
