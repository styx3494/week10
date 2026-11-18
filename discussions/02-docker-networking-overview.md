# 討論：raw/02 Docker Networking overview

## 1. 重點

1. 容器預設有網路、可以對外連線；容器只看到一張有 IP、閘道、路由表、DNS 的網卡。（開頭）
2. Linux 上 Docker 啟動時內建「default bridge」網路，沒指定 `--network` 的容器都接在上面；透過 masquerading 存取外部網路。（開頭）
3. default bridge 上的容器只能用 IP 互連、不能用名稱；自訂（user-defined）網路上可以用容器名稱互連。（User-defined networks）
4. Published ports 段落與 raw/01 相同：沒發布的連接埠主機外連不到，用 `-p` 發布。（Published ports）
5. 驅動表：bridge（預設）、host（移除與主機之間的網路隔離）、none、overlay、ipvlan、macvlan。（Drivers）
6. 子網路配置、預設位址池、DNS 細節、`container:` 網路模式。（後段）

## 2. 對應 wiki 頁

- 重點 1–3、5 → 新增 `docker-network-basics`
- 重點 4 → 補充 `docker-port-publishing` 的來源（與 raw/01 互相印證）

## 3. 衝突

- 與 raw/01 無衝突；重點 4 與 raw/01「Publishing ports」第一段文字相同。

## 4. 建議不收

- 重點 6：子網路、DNS、gateway priority 對初學者排查「網頁打不開」幫助有限。
- 驅動表只收 bridge 與 host 兩種，其他列名不展開。

## 5. 問使用者的問題

- 「預設位址池包含 192.168.0.0/16，可能與家中網段衝突」值得收嗎？→ 原文只說「may need to customize … to prevent routing conflicts」，沒有說明症狀，證據不足以寫成排錯步驟，建議不收。

## 決定（Claude 代決，待使用者確認）

- 收重點 1–5（驅動只收 bridge、host），不收 6。

## 使用者審核

- **審核結論：同意原取捨。** raw/02 說明 Linux 上未指定網路時使用 default bridge、容器預設能對外連線，以及自訂網路可用容器名稱互連。保留 bridge 與 host 的差異，並用 Published ports 段落交叉核對 raw/01。
- 位址池衝突在原文裡是可能需要調整的情境，缺少這份指南可以直接採用的診斷條件。子網路配置、DNS 細節和其他驅動維持略過。
