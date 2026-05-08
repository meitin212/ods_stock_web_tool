# ODS 股務報表統計工具

這是一個可部署在 GitHub Pages 的純前端網頁工具。使用者在瀏覽器中選擇 `.ods` 報表後，工具會在本機瀏覽器中讀取、分析、統計，並下載 Excel / CSV 結果檔。

## 功能

- 直接讀取 `.ods`、`.fods`、`.xlsx`、`.xls` 檔案。
- 自動掃描工作簿內所有 sheet，不假設固定 sheet 數。
- 自動辨識右側登打區欄位：`流水號`、`戶號`、`股數`、`登打日期`。
- 依公司、sheet、登打日期統計：
  - 總股數
  - 已繕打股戶數
- 登打日期空白時，歸入 `未填日期`。
- 每張 sheet 另產生 `TOTAL`。
- 產生異常清單，包括：未填日期、日期格式異常、有戶號但股數無效、有股數但戶號空白等。
- 不寫回原始 ODS，不覆蓋原始檔。

## 部署到 GitHub Pages

1. 建立一個 GitHub repository，例如 `ods-stock-report-tool`。
2. 上傳本資料夾內的 `index.html`、`README.md`、`.nojekyll`。
3. 到 GitHub repository 的 `Settings` → `Pages`。
4. Source 選擇 `Deploy from a branch`。
5. Branch 選擇 `main` / root。
6. 儲存後，等待 GitHub Pages 發布網址。

## 關於 SheetJS / XLSX 函式庫

目前 `index.html` 會先嘗試載入：

```text
./vendor/xlsx.full.min.js
```

如果找不到，才會改從 CDN 載入：

```text
https://cdn.jsdelivr.net/npm/xlsx@0.18.5/dist/xlsx.full.min.js
```

若報表資料敏感，建議正式部署時自行下載 `xlsx.full.min.js`，放到：

```text
vendor/xlsx.full.min.js
```

如此一來，工具頁面不需要從第三方 CDN 載入 JavaScript。

## 使用流程

1. 打開 GitHub Pages 網頁。
2. 將 ODS 檔拖曳到上傳區，或點選檔案。
3. 按「開始分析」。
4. 檢查畫面上的摘要與異常預覽。
5. 按「下載 Excel 統計結果」。

## 報表格式假設

有效報表 sheet 會優先支援下列命名：

```text
公司名稱_頁次
```

例如：

```text
中鋼_1
中鋼_2
台積電_1
```

但只要 sheet 內可辨識右側登打區欄位，仍會納入統計；若 sheet 名稱不符合 `公司_頁次` 格式，會在異常清單中提示。

## 輸出工作表

下載的 Excel 會包含：

- `總覽`
- `依公司日期統計`
- `依Sheet日期統計`
- `Sheet總表`
- `異常清單`
- `略過清單`

## 注意事項

- 工具不會自動修改原始 ODS。
- 工具不依賴 Calc 公式結果，而是從明細列重新計算。
- 若表格欄位名稱被改掉，例如 `登打日期` 改成 `日期`，該 sheet 可能無法被辨識。
- 若 ODS 檔案非常大，瀏覽器分析會需要較多記憶體與時間。
