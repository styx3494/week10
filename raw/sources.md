# 資料清單

ingest 狀態：`待收`、`討論中`、`已寫入`、`已 lint`。

網址必須自己打開確認過才能填，並優先選原廠文件。01–05 已於 2026-11-16 確認可以開啟、標題相符，並在同日存成 raw 檔。01–04 是原廠文件庫的原文，05 是結構化摘錄（見該檔檔頭）。

| 編號 | 標題 | 網址 | 取得日期 | 狀態 |
|---|---|---|---|---|
| 01 | Docker Docs：Port publishing and mapping | https://docs.docker.com/engine/network/port-publishing/ | 2026-11-16 | 已 lint |
| 02 | Docker Docs：Networking overview | https://docs.docker.com/engine/network/ | 2026-11-16 | 已 lint |
| 03 | Microsoft Learn：Enable insecure guest logons in SMB2 and SMB3 for Windows client and Windows Server | https://learn.microsoft.com/en-us/windows-server/storage/file-server/enable-insecure-guest-logons-smb2-and-smb3 | 2026-11-16 | 已 lint |
| 04 | Microsoft Learn：Detect, enable, and disable SMBv1, SMBv2, and SMBv3 in Windows | https://learn.microsoft.com/en-us/windows-server/storage/file-server/troubleshoot/detect-enable-and-disable-smbv1-v2-v3 | 2026-11-16 | 已 lint |
| 05 | Synology Knowledge Center：I cannot access a shared folder on my Synology system via SMB or AFP. What can I do? | https://kb.synology.com/en-global/DSM/tutorial/Why_cant_access_shared_folder | 2026-11-16 | 已 lint |
| 06 | （未收錄）第九週自己的筆記：Docker 網頁打不開 | 位於 week9-homework repo 的 `notes/docker-web-unreachable.html` | | 未收 |
| 07 | （未收錄）第九週自己的筆記：NAS 不在網路上 | 位於 week9-homework repo 的 `notes/nas-not-discovered.html` | | 未收 |

## 存檔方式

- 把網頁正文複製成 Markdown，存為 `raw/NN-<slug>.md`。
- 檔案開頭保留這三行：

```
來源：<網址>
取得日期：YYYY-MM-DD
說明：<這篇在講什麼，一句話>
```
