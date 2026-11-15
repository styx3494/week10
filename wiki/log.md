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

## 2026-11-16｜取得資料｜raw/01–05

- 輸入：raw/sources.md 的 5 個網址
- 變更：Docker 兩篇、Microsoft 兩篇從原廠公開的 GitHub 文件庫下載 Markdown 原文（docker/docs，Apache 2.0；MicrosoftDocs/windowsserverdocs，CC BY 4.0），存成 raw/01–04 並加上檔頭。Synology 那篇用 WebFetch 只抓到頁首和頁尾，因為正文要靠 JavaScript 才會顯示，改用瀏覽器打開並展開「For Windows PC」段落後讀取，整理成結構化摘錄 raw/05（版權屬 Synology，不存全文）
- 檢查結果：用 grep 抽查 raw/03、raw/04 的關鍵句（訪客登入風險、SMB 簽章、SMB1 預設值），都在檔案中
- 處理：無

## 2026-11-16｜Ingest 討論 ×5｜discussions/01–05

- 輸入：prompts/01-ingest-discuss.md，逐篇執行
- 討論結論：**Claude 代決，使用者未逐篇審核**。主要取捨：不收 Docker 的 direct routing、gateway modes、子網路與 DNS 細節（對初學者太進階）；開啟訪客登入的方法只記錄「有這個設定」和代價，標示不建議；Synology 的 Mac、AFP、LDAP 內容不收
- 檢查結果：討論時發現一處說法不一致。raw/05 說「Windows 10 1709 起預設停用 SMB1」，raw/04 說「Windows 10 預設不安裝 SMBv1，但 Home、Pro 例外」
- 處理：依規則把這處不一致寫進 smb-protocol-versions 的「待確認」，不自行挑選哪一邊

## 2026-11-16｜Ingest 寫入｜wiki/ 8 頁

- 輸入：prompts/02-ingest-write.md
- 變更：新增 docker-network-basics、docker-port-publishing、docker-bind-address、smb-protocol-versions、smb-guest-access、smb-signing、nas-smb-checklist、windows-smb-client-checks；更新 index.md
- 檢查結果：（見下一筆 lint）

## 2026-11-16｜Lint｜wiki/

- 輸入：prompts/03-lint.md；結構部分用腳本檢查（來源標註、raw 是否存在、斷連結、index 是否收錄、孤兒頁），來源真實性逐頁人工比對 raw 原文
- 檢查結果：
  1. 【結構】index.md 的說明文字寫了 `[[slug]]` 當範例，被當成連到不存在頁面的連結。嚴重程度：建議
  2. 【來源真實性】smb-guest-access 寫「替代做法是在 NAS 上改用帳號密碼登入」並標註 raw/03，但 raw/03 只說「升級或更換只支援訪客驗證的裝置」。這句來自先前搜尋結果的摘要，不在 raw 原文裡。**屬於把 raw 以外的資訊混進 wiki**。嚴重程度：必修
  3. 【來源真實性】smb-guest-access 寫「從 Windows 10 開始」預設不允許訪客，但 raw/03 寫的是「Windows 10 version 1709 與 Windows Server 2019」，而且 Home、Pro 版有例外。嚴重程度：必修
- 處理：1 改寫說明文字；2 拆成兩點，raw/03 只留「升級或更換」，「停用 guest、改用有權限的帳號」改標 raw/05；3 補上版本號並註明有例外。修完重跑結構檢查：無問題

## 2026-11-16｜Query：產出大綱｜slides/outline.md

- 輸入：prompts/04-query-outline.md
- 變更：產出 14 張投影片的大綱，每張都標註依據的 wiki 頁
- 檢查結果：列出 3 個 wiki 缺口，不寫進簡報：網路探索（看不到 NAS）、確認容器是否在執行的命令、Docker 主機本身的防火牆

## 2026-11-16｜檢查大綱｜slides/outline.md

- 輸入：prompts/05-outline-check.md，逐張對照 wiki 頁
- 檢查結果：
  1. 第 5 張：「L2 網段」沒有解釋，初學者看不懂 → `改大綱`，改成「接在同一台交換器（同一個 L2 網段）」，這個說法 wiki 裡就有
  2. 第 8 張：漏掉「以 Synology DSM 7 為例」和「DSM 7.2 以上」兩個限定條件 → `改大綱`
  3. 第 9 張：`net use * /delete /y` 會中斷所有網路磁碟機，大綱沒寫影響 → `改大綱`（安全檢查）
  4. 第 10 張：「Windows 11 Pro 也預設擋掉」漏了「build 25267 起」，簡化過頭就變成不精確 → `改大綱`
  5. 第 11 張：寫了「舊 NAS」，但 wiki 重點只寫「不支援簽章的第三方 SMB 伺服器」 → `改大綱`
  6. 追查第 5 點的來源，發現「舊 NAS」出自 wiki smb-signing 的「一句話說明」，那是 ingest 寫入時自己加的推測。lint 只檢查「重點」有沒有標來源，所以沒抓到 → `補 wiki`
- 處理：1–5 回到節點 4 修改大綱；6 修正 smb-signing 的一句話說明，並在 prompts/03-lint.md 新增「一句話說明不得含有重點沒有的事實」這一項（**把檢查往前移到 lint**）。修完重新逐張檢查：全部 `通過`

## 2026-11-16｜生成簡報｜slides/index.html

- 輸入：prompts/06-slides-generate.md，依據已通過檢查的 outline.md
- 變更：產出 14 張投影片的單一 HTML 檔，不使用外部套件。可用左右鍵、PageUp/PageDown、Home/End 或按鈕翻頁；網址 `#n` 可以直接連到第 n 張；支援深色模式與列印；每張投影片底部標註依據的 wiki 頁
- 檢查結果：（見下一筆）

## 2026-11-16｜檢查簡報｜slides/index.html

- 輸入：prompts/07-slides-check.md
- 檢查結果：
  1. 【事實一致】逐張比對簡報與 outline.md。第 9 張多了 `[唯讀查詢]`、`[可逆變更]` 標籤，標籤來自 wiki 頁，判定可接受；第 1 張兩個情境框的說明文字（「容器明明在跑…」「檔案總管連不上…」）是在描述症狀，沒有新增技術事實 → `通過`
  2. 【實際瀏覽】桌面淺色、手機 375px 深色都實際打開過，用 JavaScript 檢查 14 張投影片在 375px 寬時都沒有橫向溢出，主控台沒有錯誤 → `通過`
  3. 【互動】用 file:// 開啟時，Browser 頁面被包成 data: 網址，`#n` 直接跳頁測不出來。改用臨時的本機伺服器測試：`#9` 能直接跳到第 9 張；左右鍵可以翻頁；焦點在程式碼區塊上時，左右鍵留給橫向捲動、不會翻頁 → `通過`
  4. 【初學者測試】題目 2「找不到 NAS 時第一步檢查什麼」，簡報回答不出來，因為「網路探索」是大綱階段就列出的 wiki 缺口。問題出在檢查題目本身：題目是在 wiki 還沒建好前寫的，超出了 wiki 的範圍 → 修改 prompts/07 的題目，改成「打不開 NAS 共用資料夾時先查哪一端」，簡報第 8、13 張可以回答。題目 1、3 分別由第 4 張、第 7 和 12 張回答 → `通過`
- 處理：只修改了檢查題目，簡報本身不用改。臨時伺服器設定 `.claude/launch.json` 測完已刪除
