# SMB 訪客存取（Guest）

## 一句話說明

「訪客存取」是不用帳號密碼就能開共用資料夾；它很方便，但新版 Windows 預設把它擋掉，因為它不安全。

## 重點

- 從 Windows 10 version 1709 與 Windows Server 2019 開始，SMB2 與 SMB3 用戶端預設不允許用訪客帳號連到遠端伺服器，也不會在帳密錯誤後自動退回訪客；但各版本有例外，見下一點。（來源：raw/03）
- 版本差異：Windows 10 Home 與 Pro 仍預設允許訪客驗證；Windows 11 Pro（Insider Preview build 25267 起）預設不允許。（來源：raw/03）
- 開啟訪客登入的風險：可能被騙連到偽造的惡意伺服器而沒有任何警告、可能透過訪客登入執行勒索軟體等惡意程式，也容易遭中間人攻擊。（來源：raw/03）
- 微軟建議**不要**開啟不安全的訪客登入；正解是升級或更換只支援訪客驗證的裝置。（來源：raw/03）
- 開啟這個設定（群組原則或 `Set-SmbClientConfiguration -EnableInsecureGuestLogons $true`）還必須停用 SMB 簽章與加密原則，原廠說這會讓用戶端暴露在認證竊取與中繼攻擊之下。**不建議**。（來源：raw/03）
- 替代做法：升級或更換只支援訪客驗證的裝置（來源：raw/03）；在 NAS 端停用不需要的 guest 帳號，改用有 SMB 權限與資料夾權限的帳號存取（來源：raw/05）。
- NAS 端：Synology 的 guest 帳號啟用時，Windows 可能自動用訪客身分存取，因權限不足而被拒；不需要時應停用 guest 帳號。（來源：raw/05）
- 怎麼確認是這個原因：事件檢視器 Microsoft-Windows-SmbClient/Security 記錄中，事件 31017 代表「拒絕了不安全的訪客登入」。（來源：raw/03）

## 常見誤解

- 誤解：連不上 NAS，就把 Windows 的訪客登入打開。　實際上：微軟建議不要開啟（來源：raw/03）；應該用有權限的帳號連線（來源：raw/05）。

## 相關頁面

- [[smb-signing]]
- [[smb-protocol-versions]]
- [[nas-smb-checklist]]

## 待確認

- 無
