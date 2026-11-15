# LLM Wiki 規則：家用伺服器排錯

本資料夾是一份由 LLM 維護、由人審核的知識庫。主題是「家用伺服器連不上時的排錯」，涵蓋 Docker 連接埠與網路、SMB／NAS 共用、Windows 網路探索。所有簡報內容只能來自 `wiki/`。

## 目錄

- `raw/`：原始資料。放進來之後**不修改**。檔名格式 `NN-<slug>.md`，例如 `01-docker-port-publishing.md`。
- `raw/sources.md`：資料清單，記錄每篇的標題、網址、取得日期與 ingest 狀態。
- `wiki/index.md`：所有 wiki 頁面的目錄，每頁一行，附一句摘要。
- `wiki/log.md`：每次操作的紀錄，只能往下新增，不能改寫舊紀錄。
- `wiki/<slug>.md`：概念頁。slug 使用英文小寫與連字號。
- `discussions/NN-<slug>.md`：每篇 ingest 的討論輸出與決定。
- `prompts/`：流程中每個節點使用的提示詞。
- `slides/`：最後產出的 HTML 簡報。

## 頁面格式

每個概念頁都依照 `wiki/_template.md` 撰寫：

1. 第一行是 `# 頁面標題`。
2. 「一句話說明」：寫給完全不懂這個主題的人看。
3. 「重點」：條列。**每一點結尾都要標註來源**，例如 `（來源：raw/01）`。
4. 「常見誤解」與「相關頁面」：用 `[[slug]]` 連到其他頁。
5. 「待確認」：資料之間有矛盾或證據不足時寫在這裡，不可以自行選一邊。

## 硬性規則

- **先討論、後生成**：ingest 時要先執行 `prompts/01-ingest-discuss.md`，由人回覆決定後，才能執行 `02-ingest-write.md` 寫入 wiki。
- 不寫 raw 資料裡沒有的事實。LLM 自己的背景知識只能拿來提出問題，不能寫進頁面。
- 每次修改 wiki 都要同步更新 `index.md`，並在 `log.md` 新增一筆紀錄。
- 用語採臺灣繁體中文。命令、路徑、參數與專有名詞保持原文。
- 範例值固定使用：Docker 主機 `192.168.1.20`、NAS `192.168.1.50`、共用名稱 `Public`、服務名稱 `web`、主機連接埠 `8080`。

## 操作

| 操作 | 提示詞 | 何時執行 |
|---|---|---|
| Ingest：討論 | `prompts/01-ingest-discuss.md` | 每加入一篇 raw 資料 |
| Ingest：寫入 | `prompts/02-ingest-write.md` | 人審核討論結果之後 |
| Lint | `prompts/03-lint.md` | 每次 ingest 之後 |
| Query：大綱 | `prompts/04-query-outline.md` | 要做簡報時 |
| 檢查大綱 | `prompts/05-outline-check.md` | 大綱產出之後 |
| 生成簡報 | `prompts/06-slides-generate.md` | 大綱通過檢查之後 |
| 檢查簡報 | `prompts/07-slides-check.md` | 簡報產出之後 |

流程圖與重跑條件請看 `workflow.md`。
