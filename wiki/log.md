# 操作紀錄

只能往下新增，不改寫舊紀錄。這份檔案就是繳交項目 5 的「實際執行與檢查紀錄」。

## 紀錄格式

```
## YYYY-MM-DD HH:MM｜<操作>｜<對象>

- 輸入：raw/NN 或使用的提示詞
- 討論結論：我決定收／不收哪些（ingest 時填）
- 變更：新增或修改了哪些 wiki 頁
- 檢查結果：lint 或檢查發現的問題；沒有問題時寫「無」
- 處理：怎麼修、回到哪個節點重跑
```

---

## 2026-11-16｜建立骨架｜llm-wiki/

- 變更：建立 `AGENTS.md`、`raw/`、`wiki/`、`prompts/`、`workflow.md`、`reflection.md`
- 檢查結果：尚未 ingest 任何資料

## 2026-11-16｜選定資料來源｜raw/sources.md

- 輸入：用 `site:` 限定官方網域搜尋 Docker、Microsoft Learn、Synology 知識中心
- 變更：在 `raw/sources.md` 填入 01–05 的標題與網址
- 檢查結果：5 個網址都實際開啟過，標題與預期相符。Microsoft 的舊網址 `troubleshoot/.../guest-access-in-smb2-is-disabled-by-default` 會轉到新頁，因此改填轉址後的正式網址。排除 Microsoft Q&A 論壇的頁面，因為那不是原廠文件
- 處理：無
