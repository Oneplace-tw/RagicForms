# BL-001 幸福熟齡 LIFF 來源預填

- 狀態：Completed
- 完成日期：2026-09-01
- 正式環境：GitHub Pages production
- 影響範圍：`屋主需求/index.html`

## 背景

既有屋主需求 LIFF 會取得 LINE UID 與暱稱，再開啟固定的 Ragic 屋主需求表單。Ragic 來源欄位 `1004768` 預設為 `Line`，因此 LIFF 即使帶入 `pfv1004768=幸福熟齡`，舊版中繼頁未轉送參數時仍會顯示 `Line`。

## 已完成

1. 同一個 LIFF App 可接受 `pfv1004768=幸福熟齡`。
2. 僅允許 allowlist 中的 `幸福熟齡` 被轉送。
3. 無參數或非法來源值時不加入 `pfv1004768`，保持既有 Ragic 預設來源 `Line`。
4. 既有 LIFF ID、Ragic 路徑、LINE UID／暱稱欄位與外部開窗行為皆未變更。

## 正式驗證證據

- Pull request：[#2](https://github.com/Oneplace-tw/RagicForms/pull/2)
- Merge commit：`9f000e5dee6eed9c04ee7b3a935c0246c44168d4`
- GitHub Pages build：`built`
- Build 完成時間：2026-09-01T11:10:58Z
- 正式頁面與 `main` SHA-256：`7af2aad532b566d31c635dd7a7bf61e917bdc2bbcf2506c456c79b32d24e5a81`
- 正式函式驗證：幸福熟齡會加入來源；舊入口及非法來源不會加入來源。
- Ragic 預填驗證：欄位 `1004768` 的選取值、`data-value` 與顯示文字皆為 `幸福熟齡`。
- 驗證過程未送出表單，未新增測試紀錄。

## 正式入口

```text
https://liff.line.me/2006833424-920EB8ra/?pfv1004768=%E5%B9%B8%E7%A6%8F%E7%86%9F%E9%BD%A1
```

## 回退方式

Revert PR #2 的 merge commit，即可恢復原本固定只轉送 LINE UID 與暱稱的行為。
