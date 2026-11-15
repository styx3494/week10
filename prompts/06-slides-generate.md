# 節點 6：生成 HTML 簡報

依照已通過檢查的 `llm-wiki/slides/outline.md`，產出 `llm-wiki/slides/index.html`：

- 單一 HTML 檔，CSS 與 JS 寫在檔案裡，不使用外部套件，可以離線開啟，也可以放上 GitHub Pages。
- 每張投影片是一個 `<section>`。可以用左右方向鍵和按鈕切換，並顯示頁碼。
- 手機上也能閱讀。程式碼區塊可以橫向捲動。
- 每張投影片底部用小字標註依據的 wiki 頁。
- **不可以新增大綱裡沒有的事實。** 只能調整文字、排版與舉例方式。
- 範例 IP 與名稱依照 `AGENTS.md` 的固定範例值。
