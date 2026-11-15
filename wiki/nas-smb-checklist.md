# NAS 端 SMB 檢查清單

## 一句話說明

電腦打不開 NAS 的共用資料夾時，先到 NAS 那一端確認「門有開、人有權限、沒被封鎖」。

## 重點

以下以 Synology DSM 7 為例；其他品牌的選單名稱不同，請查自家 NAS 的文件。

- NAS 與電腦在同一個區域網路（LAN），而且 NAS 使用固定的 LAN IP，例如 `192.168.1.50`。（來源：raw/05）
- NAS 的防火牆沒有擋住 SMB 用的連接埠 137–139 與 445。（來源：raw/05）
- 磁碟區狀態為 Normal；要存取的共用資料夾存在，有加密的話已經掛載。（來源：raw/05）
- 已在 Control Panel > File Services 啟用 SMB。（來源：raw/05）
- 使用的帳號有 SMB 應用程式權限（Control Panel > Application Privileges），也有該共用資料夾的存取權限。（來源：raw/05）
- 不需要 guest 帳號時應停用。（來源：raw/05）
- DSM 7.2 以上若啟用了自動封鎖（auto block），檢查電腦的 IP 有沒有被列進 Block List。（來源：raw/05）
- SMB 最大／最小協定版本符合電腦需求，建議最大 SMB3、最小 SMB2。（來源：raw/05）

## 常見誤解

- 誤解：要從外面存取 NAS，就在路由器設連接埠轉發。　實際上：原廠指出把連接埠開放到網際網路有安全風險，建議改用 VPN。（來源：raw/05）

## 相關頁面

- [[windows-smb-client-checks]]：電腦端要檢查什麼
- [[smb-guest-access]]
- [[smb-protocol-versions]]

## 待確認

- 無
