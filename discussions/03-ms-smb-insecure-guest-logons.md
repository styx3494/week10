# 討論：raw/03 Enable insecure guest logons in SMB2 and SMB3

## 1. 重點

1. Windows 10 起 SMB2/3 用戶端預設不允許訪客（Guest）存取，也不會在帳密錯誤後退回訪客。（Default behaviors）
2. 版本差異：Windows 10 Home、Pro 仍預設允許；Windows 11 Pro（Insider build 25267 起）預設不允許；Windows 11 24H2 與 Windows Server 2025 起預設要求 SMB 簽章，訪客驗證可能因簽章失敗而無法連線。（Default behaviors）
3. 開啟訪客登入的風險：可能被騙連到偽造伺服器、透過訪客登入執行惡意程式（如勒索軟體）、遭中間人攻擊。微軟建議**不要**開啟。（Caution）
4. 原廠建議：升級或更換只支援訪客驗證的第三方裝置。（開頭）
5. 開啟方式：gpedit 的 Lanman Workstation 原則，或 `Set-SmbClientConfiguration -EnableInsecureGuestLogons $true -Force`；需要停用 SMB 簽章與加密原則。（Enable insecure guest logons）
6. 事件記錄：31017（拒絕訪客登入）等事件 ID。（Audit）

## 2. 對應 wiki 頁

- 重點 1–5 → 新增 `smb-guest-access`
- 重點 2 的簽章部分 → 新增 `smb-signing`
- 重點 6 → 收進 `smb-guest-access` 作為「怎麼確認是這個原因」

## 3. 衝突

- 與現有 wiki 無衝突。

## 4. 建議不收

- 網域群組原則（gpmc.msc）細節：家用情境不適用。

## 5. 問使用者的問題

- 開啟方式（重點 5）要不要寫？→ 建議只寫「存在這個設定」與代價，**不寫成推薦步驟**，並在頁面明確標「不建議」。

## 決定（Claude 代決，待使用者確認）

- 收 1–4、6；重點 5 只記錄存在與代價，標示不建議。

## 使用者審核

- **審核結論：維持收錄預設行為、版本差異、風險與事件 31017。** 依 raw/03 的 Default behaviors，保留 Windows 10 version 1709、Windows Server 2019、Windows 10 Home／Pro 例外和 Windows 11 Pro Insider Preview build 25267。訪客驗證與簽章相容性由簽章頁承接。
- **修正寫法。** 原決定只記設定存在與代價，但 wiki 仍有能直接啟用的 PowerShell 指令。移除指令，保留所需停用的保護、微軟的風險說明與升級／更換裝置的建議。維持不收網域群組原則細節。
