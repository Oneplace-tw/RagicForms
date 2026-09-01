# BL-001 幸福熟齡 LIFF 來源預填

- 狀態：In Progress
- 目標環境：GitHub Pages production
- 影響範圍：`屋主需求/index.html`

## 背景

既有屋主需求 LIFF 會取得 LINE UID 與暱稱，再開啟固定的 Ragic 屋主需求表單。Ragic 來源欄位 `1004768` 預設為 `Line`，因此 LIFF 即使帶入 `pfv1004768=幸福熟齡`，現有中繼頁未轉送參數時仍會顯示 `Line`。

## 已驗證現況

- LIFF ID：`2006833424-920EB8ra`
- Ragic 路徑：`/OnePlaceLiving/development-department/1`
- LINE UID 欄位：`1002801`
- LINE 暱稱欄位：`1010838`
- 來源欄位：`1004768`
- Ragic 已存在選項：`幸福熟齡`
- 直接使用 Ragic `pfv1004768=幸福熟齡` 時可正確預填。
- 現有 LIFF 無參數入口必須維持 Ragic 預設來源 `Line`。

## 需求

1. 同一個 LIFF App 可接受 `pfv1004768=幸福熟齡`。
2. 僅允許明確列入 allowlist 的來源值被轉送。
3. 無參數或非法來源值時，不加入 `pfv1004768`，保持既有行為。
4. 不改變既有 LIFF ID、Ragic 路徑、LINE UID／暱稱欄位或外部開窗行為。

## 驗收條件

- 無 query string 時，產生的 Ragic URL 與修改前完全一致。
- `?pfv1004768=幸福熟齡` 時，最終 Ragic URL 包含 URL encoded 的 `pfv1004768=幸福熟齡`。
- 非 allowlist 值不會出現在最終 Ragic URL。
- LINE UID 與暱稱仍正確寫入既有欄位。
- GitHub Pages build 成功，正式頁面內容與 main commit 一致。

## 回退方式

Revert 本 BL 的實作 commit，即可恢復原本固定只轉送 LINE UID 與暱稱的行為。
