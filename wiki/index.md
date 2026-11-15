# Wiki 目錄

每頁一行：雙中括號頁名連結、一句摘要、來源編號。依分類排列。

## Docker

- [[docker-network-basics]]：容器預設接在 bridge 網路，能對外連線，但外面連不進來（raw/02）
- [[docker-port-publishing]]：用 `-p 主機:容器` 發布連接埠，主機外面才連得到（raw/01、raw/02）
- [[docker-bind-address]]：發布到 `0.0.0.0` 誰都連得到，綁 `127.0.0.1` 只有主機自己（raw/01）

## NAS・區域網路

- [[smb-protocol-versions]]：SMB1 不安全且新版 Windows 預設不裝，NAS 建議 SMB2～SMB3（raw/04、raw/05）
- [[smb-guest-access]]：新版 Windows 預設擋掉訪客登入，微軟建議不要打開（raw/03、raw/05）
- [[smb-signing]]：Windows 11 24H2 起預設要求簽章，不支援的舊 NAS 可能連不上（raw/03、raw/04）

## 排錯方法

- [[nas-smb-checklist]]：NAS 端檢查清單：網路、防火牆、SMB 開關、權限、guest、封鎖、協定範圍（raw/05）
- [[windows-smb-client-checks]]：Windows 端檢查：IP 與名稱、舊認證、重複連線（raw/05）
