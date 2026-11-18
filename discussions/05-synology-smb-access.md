# 討論：raw/05 Synology：無法透過 SMB 存取共用資料夾

## 1. 重點

1. NAS 端檢查清單：網路正常、同一個 LAN、固定 IP、防火牆沒擋 137-139/445、磁碟區 Normal、共用資料夾存在、已啟用 SMB、帳號有 SMB 應用程式權限與資料夾權限、自動封鎖沒封到用戶端 IP。（On your Synology system）
2. guest 帳號啟用時，Windows 可能自動用訪客身分連線而被拒；不需要時應停用。（第 11 項與註 5）
3. SMB 協定範圍：最大 SMB3、最小 SMB2；Windows 10 1709 起預設停用 SMB1。（第 13 項與註 6）
4. 從網際網路存取需要連接埠轉發，但原廠指出有安全風險、建議用 VPN。（第 5 項與註 2）
5. Windows 端：清除認證管理員中的舊認證、用 IP 與名稱分別連線、`ping` 名稱比對 IP、`nbtstat -R`、`net use * /delete /y`。（For Windows PC）

## 2. 對應 wiki 頁

- 重點 1 → 新增 `nas-smb-checklist`
- 重點 2 → 補充 `smb-guest-access`（NAS 端觀點）
- 重點 3 → 補充 `smb-protocol-versions`
- 重點 4 → 收進 `nas-smb-checklist` 的「常見誤解」
- 重點 5 → 新增 `windows-smb-client-checks`

## 3. 衝突

- raw/05 註 6 說「SMB1 is disabled by default since Windows 10 version 1709」；raw/04 說「SMBv1 isn't installed by default in Windows 10, except Home and Pro editions」。**說法不一致**：raw/05 沒提 Home、Pro 例外。以原廠作業系統文件 raw/04 為準，但依規則寫進「待確認」，不自行刪除任一方。

## 4. 建議不收

- Mac、AFP、LDAP、網域、變音字母使用者名稱：與本主題（Windows 連家用 NAS）無關。
- `nbtstat -r/-A/-a/-c`（聯絡技術支援用）：不收。

## 5. 問使用者的問題

- raw/05 是結構化摘錄，不是全文。這樣可以嗎？→ 原文版權屬 Synology、頁面需 JavaScript 才能顯示，建議接受，已在 raw 檔頭註明。

## 決定（Claude 代決，待使用者確認）

- 收 1–5；SMB1 預設值的不一致寫進 `smb-protocol-versions` 的「待確認」。

## 使用者審核

- **審核結論：保留 NAS 與 Windows 兩端的檢查。** raw/05 是逐段整理的來源摘錄，足以支撐 DSM 權限、guest、自動封鎖、SMB2～SMB3 和 Windows 舊認證等檢查。保留 `nbtstat -R`，適用於 IP 可連、名稱不可連且名稱對到錯誤 IP 的情境。`net use * /delete /y` 須保留中斷所有網路磁碟機對應的提醒。維持略過 Mac、AFP、LDAP、網域和技術支援用的延伸命令。
- **修正 SMB1 的裁定。** Synology 註 6 說 Windows 10 version 1709 起預設停用；Microsoft 談的是預設未安裝，並列 Home／Pro 例外。保留來源差異與待確認項，排錯時以實際 Windows 版本、版本別與功能狀態核對。NAS 設定建議仍是最小 SMB2、最大 SMB3。
