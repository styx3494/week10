來源：https://kb.synology.com/en-global/DSM/tutorial/Why_cant_access_shared_folder
取得日期：2026-11-16
說明：從 NAS 端與 Windows 端排查「無法透過 SMB 存取 Synology 共用資料夾」
授權：Synology 版權所有，未採開放授權
形式：**結構化摘錄，不是全文。** 頁面需以瀏覽器執行 JavaScript 才會顯示內容，因此依原文段落順序整理成條列；選單路徑與命令保留原文。適用：DSM 7 series、DSM legacy versions、DSM Enterprise (PAS)。頁面標示 Last updated: Apr 9, 2026。

---

# I cannot access a shared folder on my Synology system via SMB or AFP. What can I do?（摘錄）

## Symptoms

- 無法透過 SMB 或 AFP 存取共用資料夾。

## Resolution：On your Synology system（逐項確認）

1. Synology 系統與網路連線正常。
2. Synology 系統與用戶端電腦位於同一個 LAN。
3. Synology 系統使用固定（static）的 LAN IP。
4. DSM 6.2 以上的防火牆沒有擋住 SMB（137-139、445）或 AFP（548）連接埠。
5. 若要從網際網路存取，路由器上必須設定好 SMB 或 AFP 的連接埠轉發。（註 2：開放連接埠到網際網路有安全風險，原廠建議改用 VPN；若一定要轉發，最小 SMB 設為 SMB2、最大設為 SMB3，Transport encryption mode 設為 Force。）
6. 磁碟區（Volume）狀態為 Normal。DSM 7：Storage Manager > Storage > Storage Pool > Volume。
7. 要存取的共用資料夾存在於 Control Panel > Shared Folder；若有加密，須已掛載。
8. 已在 Control Panel > File Services 啟用 SMB 或 AFP。
9. 使用者帳號在 Control Panel > Application Privileges 有 SMB 或 AFP 的應用程式權限（DSM 7.0 以上）。
10. 使用者帳號有該共用資料夾的存取權限。（註 4：可用管理員帳號登入 File Station 檢查與調整權限。）
11. 不再需要 guest 帳號時必須停用。DSM 7：Control Panel > User & Group > User。（註 5：guest 帳號啟用時，電腦可能自動以訪客身分存取，因權限不足而被拒絕。）
12. DSM 7.2 以上：Control Panel > Security > Protection，若啟用了 auto block，檢查用戶端 IP 是否在 Block List 中，必要時移除或加入 Allow List。
13. SMB 最大／最小協定版本符合用戶端需求。可將最大設為 SMB3，最小設為 SMB2 以提升安全性。DSM 7：Control Panel > File Services > SMB > Advanced Settings。（註 6：SMB3 向下相容 SMB2，且比 SMB1 安全；Windows 10 1709 起預設停用 SMB1，對 Windows 10 電腦應將最小協定設為 SMB2；部分舊裝置如 Windows XP、多功能印表機、IP 攝影機只支援 SMB1。）

## Resolution：On your client computer — For Windows PC

1. 若要使用 SMB 檔案服務，避免用 Windows Hello 登入 Windows。（註 7：某些 Windows 版本啟用 Windows Hello 時無法對應網路磁碟機，可更新 Windows、修改使用者名稱或停用 Windows Hello。）
2. 嘗試用 Synology Assistant 對應網路磁碟機。
3. 重設已儲存的認證：Control Panel > User Accounts > Credential Manager > Windows Credentials，刪除所有與該 Synology 相關（IP 與伺服器名稱）的認證後重新連線。若清單是空的仍連不上，改為 Add a Windows credential，輸入 IP 或伺服器名稱、帳號、密碼。
4. 在檔案總管分別用 IP 與伺服器名稱連線。若 IP 可以、名稱不行，在命令提示字元執行：

   ```
   ping Server name of Synology system
   ```

   確認 `Reply from` 後面的 IP 與 Synology 的 IP 相同。不同的話執行下列命令或重新開機後再試：

   ```
   nbtstat -R
   ```

5. 確認同一台電腦沒有用不同帳號同時連到這台 Synology。關閉所有檔案總管視窗，執行下列命令移除所有已對應的網路磁碟機，再重新設定：

   ```
   net use * /delete /y
   ```

6. Synology 加入網域時，改用其他帳號類型（本機帳號或網域帳號）存取。
7. 以上都無效時，執行 `nbtstat -r`、`nbtstat -A <IP>`、`nbtstat -a <名稱>`、`nbtstat -c`，截圖後聯絡原廠技術支援。

## 其他註記

- Windows 檔案總管無法以 UNC 路徑連到名稱以句點（.）結尾的共用資料夾。
