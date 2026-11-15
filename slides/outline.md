# 簡報大綱：家用伺服器連不上時，怎麼一步一步排查？

聽眾：完全不懂 Docker、NAS、網路的初學者。依據：只使用 `wiki/`。

## 1. 標題頁
- 家用伺服器連不上時，怎麼一步一步排查？
- 兩個最常見的情況：Docker 架的網頁打不開、NAS 的共用資料夾打不開
- 依據：index

## 2. 先建立一個比喻：房間與門
- 容器像主機裡的小房間，房門預設是關著的
- 連不上，通常是「門沒開」「門只對自己開」或「門口有人擋」
- 依據：docker-port-publishing（一句話說明）、docker-bind-address（一句話說明）、nas-smb-checklist（一句話說明）

## 3. Docker 的網路長什麼樣子
- 容器預設就有網路，可以主動對外連線
- 沒有指定網路時，容器接在內建的 default bridge 網路上
- 能對外連線，不代表外面連得進來
- 依據：docker-network-basics

## 4. 開門：用 `-p` 發布連接埠
- 沒有發布的連接埠，主機外面的裝置連不到
- `-p 8080:80`：前面是主機（8080），後面是容器（80）
- 預設是 TCP，UDP 要寫 `/udp`
- 依據：docker-port-publishing

## 5. 門開給誰：`0.0.0.0` 與 `127.0.0.1`
- 沒寫位址：發布到主機所有位址，原廠說「預設不安全」，外面也連得到
- 寫 `127.0.0.1:8080:80`：只有 Docker 主機自己連得到
- 注意：Docker 28.0.0 以前，接在同一台交換器（同一個 L2 網段）的主機，仍可能連到綁在 localhost 的連接埠
- 依據：docker-bind-address

## 6. Docker 網頁打不開：排查三問
- 啟動時有沒有加 `-p`？
- 主機與容器的連接埠有沒有寫反？
- 是不是綁在 `127.0.0.1`，所以只有主機自己連得到？
- 依據：docker-port-publishing（常見誤解）、docker-bind-address（常見誤解）

## 7. SMB 是什麼？為什麼不要用 SMB1
- SMB 是 Windows 開共用資料夾用的「語言」，有 SMB1、SMB2、SMB3
- SMB1 有重大安全弱點，微軟強烈建議不要用；Windows 11 預設沒有安裝
- NAS 建議設定：最大 SMB3、最小 SMB2
- 依據：smb-protocol-versions

## 8. NAS 端檢查清單
- 以 Synology DSM 7 為例，其他品牌的選單名稱不同
- 同一個 LAN、NAS 有固定 IP（例如 `192.168.1.50`）
- 防火牆沒擋 137–139、445；已啟用 SMB
- 帳號有 SMB 權限與資料夾權限；不需要的 guest 帳號已停用；DSM 7.2 以上確認 IP 沒被自動封鎖
- 依據：nas-smb-checklist

## 9. Windows 端檢查
- 分別用 IP（`\\192.168.1.50\Public`）和名稱連線，比較結果
- IP 可以、名稱不行：`ping <NAS 名稱>` 看回應的 IP 對不對
- 被拒絕：到認證管理員清除舊的 NAS 認證（之後要重新輸入帳密）
- 有重複連線：`net use * /delete /y` 會中斷**所有**網路磁碟機，之後要重新對應
- 依據：windows-smb-client-checks

## 10. 為什麼 Windows 擋掉訪客登入
- 訪客登入 = 不用帳密就能進共用資料夾
- Windows 10 1709 起預設擋掉（Home、Pro 版有例外）；Windows 11 Pro 自 build 25267 起也預設擋掉
- 風險：被騙連到假伺服器、勒索軟體、中間人攻擊
- 微軟建議不要打開；改用有權限的帳號，或更換只支援訪客的舊裝置
- 依據：smb-guest-access

## 11. Windows 11 24H2 的新門檻：SMB 簽章
- 簽章 = 封包上的防偽章
- 24H2 起預設要求簽章，不支援簽章的第三方 SMB 伺服器、訪客共用、工作群組電腦可能連不上
- 改 SMB 版本不會改變簽章要求；不要用停用簽章來繞過
- 依據：smb-signing

## 12. 三個常見誤解
- 「容器跑起來了，網頁就一定打得開」→ 沒發布連接埠就連不到
- 「連不上 NAS 就打開訪客登入」→ 微軟建議不要
- 「升級 24H2 後連不上，打開 SMB1 就好」→ 簽章要求與版本無關
- 依據：docker-port-publishing、smb-guest-access、smb-signing（常見誤解）

## 13. 總結：排查順序與安全原則
- Docker：有沒有開門（`-p`）→ 門有沒有開對（順序）→ 門開給誰（綁定位址）
- NAS：先查 NAS 端清單 → 再查 Windows 端
- 安全原則：不開 SMB1、不開訪客登入；要從外面連，原廠建議用 VPN 而不是連接埠轉發
- 依據：docker-port-publishing、docker-bind-address、nas-smb-checklist、windows-smb-client-checks、smb-protocol-versions、smb-guest-access

## 14. 參考資料
- raw/01–05 的原廠文件
- 依據：raw/sources.md

## wiki 缺口（不寫進簡報）
- 「在網路芳鄰看不到 NAS」（網路探索）：wiki 沒有資料
- 「確認容器有沒有在執行」的命令（例如查看容器清單）：wiki 沒有資料
- Docker 主機本身的防火牆：wiki 沒有資料
