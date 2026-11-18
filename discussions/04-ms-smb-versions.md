# 討論：raw/04 Detect, enable, and disable SMBv1, SMBv2, and SMBv3

## 1. 重點

1. SMBv1 有重大安全弱點，微軟強烈建議不要使用；Windows 11 任何版本預設都沒安裝 SMBv1，Windows 10 除 Home、Pro 外也沒安裝。（開頭）
2. 建議更新仍需要 SMB1 的 SMB 伺服器，而不是在電腦上裝回 SMBv1。（開頭）
3. Windows 11 24H2 與 Windows Server 2025 預設要求 SMB 簽章，可能連不上工作群組電腦、訪客共用或不支援簽章的第三方 SMB 伺服器；改變啟用的 SMB 版本不會改變簽章要求；不要停用 SMB 版本或簽章來繞過，應在遠端伺服器啟用簽章或更新／更換裝置。（開頭第二段）
4. 不需系統管理員權限即可偵測：`Get-SmbServerConfiguration | Format-List EnableSMB1Protocol`。（Tip）
5. 用 `Enable-/Disable-WindowsOptionalFeature` 啟用或停用 SMB1 後電腦會重新開機。（Use PowerShell to remove SMBv1）
6. SMBv2／v3 停用會失去的功能清單；登錄檔與群組原則的作法。（中後段）

## 2. 對應 wiki 頁

- 重點 1、2、4、5 → 新增 `smb-protocol-versions`
- 重點 3 → 補進 `smb-signing`（與 raw/03 互相印證）

## 3. 衝突

- 與 raw/03 對照：raw/03 說「Windows 10 Home、Pro 仍允許訪客」，raw/04 說「Windows 10 Home、Pro 仍有安裝 SMBv1」。兩者講的是不同設定，**不是矛盾**，但容易混淆，頁面上要分開寫。

## 4. 建議不收

- 重點 6：登錄檔、群組原則、SMBv2/v3 功能清單，對初學者太細。

## 5. 問使用者的問題

- `Get-SmbServerConfiguration` 偵測的是**這台電腦作為 SMB 伺服器**的設定，不是連到 NAS 的用戶端。要不要收？→ 建議收，但註明它查的是伺服器端，避免讀者誤用。

## 決定（Claude 代決，待使用者確認）

- 收 1–5，不收 6；偵測命令註明「查的是本機作為伺服器的設定」。

## 使用者審核

- **審核結論：收安全風險、原廠建議、本機查詢和重新開機提醒。** `Get-SmbServerConfiguration` 查的是本機 SMB 伺服器設定。重新開機的提醒應限定在用 Windows 選用功能的 PowerShell 命令安裝或移除 SMBv1。保留 SMB 簽章的獨立要求，略過登錄檔、群組原則和 SMB2／SMB3 功能清單。
- **修正預設值表述。** raw/04 的 Home／Pro 例外表示文件的通則有適用界線，不能從例外倒推出每個 Windows 10 Home／Pro 組建都已安裝 SMBv1。與 raw/05 的不同措辭一併留在「待確認」。
