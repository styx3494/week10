# LLM Wiki：家用伺服器排錯

**主題簡介**：初學者在家裡架設 Docker 服務或 NAS 時，常會遇到「網頁打不開」「找不到 NAS」「共用資料夾拒絕存取」等問題。這份 Wiki 從 Docker、Microsoft 與 NAS 廠商的原廠文件整理出觀念，最後產出一份教學 HTML 簡報：「家用伺服器連不上時，怎麼一步一步排查？」

## 進度

- [x] ingest 5 篇資料（見 `raw/sources.md`），產出 8 頁 wiki
- [x] lint，修正 2 個必修問題
- [x] 產出簡報大綱並通過檢查（修正 6 個問題）
- [x] 產出 `slides/index.html` 並通過檢查
- [x] `reflection.md` 草稿
- [ ] **使用者審核**：逐篇確認 `discussions/` 中由 Claude 代做的決定，並改寫反思
- [ ] push 到 GitHub，開啟 GitHub Pages

## 怎麼使用

1. 把一篇資料存成 `raw/NN-<slug>.md`，並登記到 `raw/sources.md`。
2. 把 `prompts/01-ingest-discuss.md` 的內容貼給 AI，再把 `NN` 換成這篇的編號。
3. 閱讀 AI 的討論結果，回覆要收哪些、不收哪些。這一步就是「先討論」。
4. 執行 `prompts/02-ingest-write.md`，讓 AI 寫入 wiki，再執行 `03-lint.md`。
5. 重複 1–4，直到收完 5 篇。
6. 依序執行 04 → 05 → 06 → 07，產出簡報。

## 繳交對照

| 繳交項目 | 位置 |
|---|---|
| 1. 主題與簡介 | 本檔開頭 |
| 2. Wiki 成果 | `wiki/` |
| 3. 教學簡報 | `slides/index.html`（GitHub Pages） |
| 4. loop / graph | `workflow.md` |
| 5. 執行與檢查紀錄 | `wiki/log.md`、`discussions/` |
| 6. 反思 | `reflection.md` |
