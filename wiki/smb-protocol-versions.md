# SMB 協定版本（SMB1／SMB2／SMB3）

## 一句話說明

SMB 是 Windows 開共用資料夾用的「語言」，有好幾個版本；最舊的 SMB1 有嚴重安全問題，新版 Windows 預設已經不裝了。

## 重點

- SMBv1 有重大安全弱點，微軟強烈建議不要使用。（來源：raw/04）
- Windows 11 所有版本與 Windows Server 2019 之後，預設都沒有安裝 SMBv1；Windows 10 也沒有，但 Home 與 Pro 版例外。（來源：raw/04）
- 微軟建議更新仍需要 SMB1 的 SMB 伺服器，而不是在電腦上把 SMBv1 裝回來。（來源：raw/04）
- `[唯讀查詢]` 不需系統管理員權限就能查看這台電腦**作為 SMB 伺服器**是否啟用 SMB1：`Get-SmbServerConfiguration | Format-List EnableSMB1Protocol`。注意它查的不是連到 NAS 的用戶端設定。（來源：raw/04）
- 用 PowerShell 啟用或停用 SMB1 功能後，電腦會重新開機。（來源：raw/04）
- NAS 端建議：SMB 最大協定設為 SMB3、最小設為 SMB2；SMB3 向下相容 SMB2，且比 SMB1 安全。（來源：raw/05）
- 部分舊裝置（例如 Windows XP、多功能印表機、IP 攝影機）只支援 SMB1。（來源：raw/05）

## 常見誤解

- 誤解：SMB1 只是比較舊，打開來相容性比較好。　實際上：微軟因為安全弱點強烈建議不要使用。（來源：raw/04）

## 相關頁面

- [[smb-signing]]
- [[smb-guest-access]]
- [[nas-smb-checklist]]

## 待確認

- Windows 10 的 SMB1 預設值說法不一致：raw/05（Synology）寫「Windows 10 1709 起預設停用 SMB1」，未提例外；raw/04（Microsoft）寫「Windows 10 預設不安裝 SMBv1，但 Home 與 Pro 例外」。作業系統行為以原廠 raw/04 為準，但兩者並存，待使用者確認是否要在簡報中提到 Windows 10 的版本差異。
