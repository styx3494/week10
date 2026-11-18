# 繳交內容（可直接貼上）

**標題**：`<學校> <學號> <系級> <姓名> 家用伺服器排錯 LLM Wiki`

---

## 1. LLM Wiki 主題與簡短介紹

主題：家用伺服器排錯。初學者在家架設 Docker 服務或 NAS 時，常遇到「網頁打不開」「共用資料夾打不開或拒絕存取」。這份 Wiki ingest 了 5 篇原廠文件（Docker 2 篇、Microsoft 2 篇、Synology 1 篇），整理成 8 頁概念頁，每個重點都標註原始資料來源。

## 2. LLM Wiki 連結

- 首頁：https://styx3494.github.io/week10/
- Wiki 內容：https://github.com/styx3494/week10/tree/main/wiki
- 原始資料：https://github.com/styx3494/week10/tree/main/raw

## 3. 教學 HTML 簡報連結

https://styx3494.github.io/week10/slides/

## 4. loop / graph 流程

取得資料 → 討論重點（人審核）→ 寫入 Wiki → Lint 檢查 →（重複 5 篇）→ 查詢 Wiki 整理大綱 → 檢查大綱 → 生成 HTML 簡報 → 檢查簡報 → 發布

- 會重複的步驟：每篇資料都跑一次「取得 → 討論 → 寫入 → lint」；大綱、簡報不合格時退回重做。
- 需要檢查或重新生成的地方：人審核討論結果、lint（來源與連結）、檢查大綱（每點能追溯到 wiki）、檢查簡報（沒有新增事實、版面正常）。
- 為什麼這樣設計：越早檢查，重做的範圍越小；每一層都標註上一層的來源，才能一路往回對。

流程圖與修改紀錄：https://github.com/styx3494/week10/blob/main/workflow.md

## 5. 一次實際執行的結果與檢查紀錄

- 操作紀錄：https://github.com/styx3494/week10/blob/main/wiki/log.md
- 五篇 ingest 的討論與審核：https://github.com/styx3494/week10/tree/main/discussions

摘要：lint 抓到 2 個必修問題（其中一句不在原文裡，是從搜尋結果摘要混進來的）；檢查大綱抓到 6 個問題；簡報實際在瀏覽器以桌面與手機寬度檢查；審核後再修訂 wiki 並重跑 lint。

## 6. 反思：哪個節點最常出錯？如何調整檢查流程？

https://github.com/styx3494/week10/blob/main/reflection.md

（建議把 reflection.md 第 1、2 題的重點各摘一兩句貼在這裡。）
