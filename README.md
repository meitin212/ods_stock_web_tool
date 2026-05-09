# ODS 股務報表統計工具｜輕量版

這是一個可部署在 GitHub Pages 的純前端網頁工具。使用者選擇 `.ods` 報表後，工具會在本機瀏覽器中讀取、分析、統計，並下載結果檔。

## v0.2.0-lightweight 重點

- 不使用 SheetJS / XLSX 函式庫。
- 不使用 CDN。
- 直接解壓縮 ODS 內的 `content.xml`，逐張 sheet 掃描需要的欄位。
- 適合處理大型 LibreOffice Calc 檔，例如 `content.xml` 超過 100MB 的情況。
- 原始 ODS 不會上傳、不會修改、不會覆蓋。

## 功能

- 自動掃描所有 sheet，不假設固定 sheet 數。
- 自動辨識右側登打區欄位：`流水號`、`戶號`、`股數`、`登打日期`。
- 依公司、sheet、登打日期統計：
  - 總股數
  - 已繕打股戶數
- 登打日期空白時，列入「未填日期」。
- 產生：
  - 總覽
  - 依公司日期統計
  - 依 Sheet 日期統計
  - Sheet 總表
  - 異常清單
  - Sheet 處理狀態

## 輸出格式

目前輸出為 Excel 2003 XML 格式，副檔名 `.xls`。LibreOffice Calc 與 Microsoft Excel 均可開啟。

若只需要單張資料，也可下載 CSV。

## 部署到 GitHub Pages

1. 建立 GitHub repository。
2. 上傳 `index.html`、`README.md`、`.nojekyll`。
3. 到 GitHub repository 的 `Settings` → `Pages`。
4. Source 選擇 `Deploy from a branch`。
5. Branch 選擇 `main` / root。
6. 等待 GitHub Pages 發布。

## 瀏覽器需求

需要支援 `DecompressionStream` 的現代瀏覽器。建議使用新版 Chrome、Edge 或 Firefox。

## 注意

這個版本以穩定處理大型 ODS 為優先，因此不保留原始格式，也不輸出真正的 `.xlsx`。若後續需要美化輸出或產生 `.xlsx`，可在此版本穩定後再擴充。
