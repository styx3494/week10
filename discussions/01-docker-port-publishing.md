# 討論：raw/01 Docker Port publishing and mapping

## 1. 重點

1. 沒有發布的連接埠，Docker 預設會擋掉；bridge 網路上的容器連接埠只有 Docker 主機與同網路的容器連得到，主機外面連不到。（Publishing ports 第一段）
2. `-p 8080:80` 把主機所有位址的 8080 對應到容器的 TCP 80；可以加主機 IP 限定，`/udp` 指定 UDP。（Publishing ports 表格）
3. 發布連接埠「預設不安全」：不只主機，外面的世界也連得到；加上 `127.0.0.1` 只有 Docker 主機連得到。28.0.0 之前的版本，同一個 L2 網段的主機仍連得到發布在 localhost 的連接埠。（IMPORTANT／WARNING 方塊）
4. 沒寫主機位址時，預設發布到所有主機位址（`0.0.0.0` 與 `[::]`）；可用 daemon 設定改成預設只綁 `127.0.0.1`。（Setting the default bind address）
5. Direct routing、gateway modes（nat、routed、isolated…）、SNAT。（中後段）

## 2. 對應 wiki 頁

- 重點 1、2 → 新增 `docker-port-publishing`
- 重點 3、4 → 新增 `docker-bind-address`（發布範圍：誰連得到）

## 3. 衝突

- 目前 wiki 是空的，無衝突。

## 4. 建議不收

- 重點 5（direct routing、gateway modes、SNAT、IPv6 細節）：家用初學者情境用不到，太進階。

## 5. 問使用者的問題

- 28.0.0 之前版本的 localhost 漏洞警告要不要收？→ 建議收在 `docker-bind-address` 的「常見誤解」，因為讀者可能以為綁 127.0.0.1 就一定安全。

## 決定（Claude 代決，待使用者確認）

- 收重點 1–4，不收 5。警告收進「常見誤解」。

## 使用者審核

- **審核結論：保留重點 1–4，維持不收重點 5。** raw/01 的 bridge 段落和發布表格足以解釋主機內外的可達性、`-p` 兩側的連接埠及 TCP／UDP。direct routing、gateway modes 和 SNAT 可留給進階情境。
- **修正寫法。** raw/01 的警告明列 Docker 28.0.0 以前的同一 L2 網段例外。保留「常見誤解」的說明，也把例外帶進綁定 localhost 的重點，避免讀者只看重點就誤判暴露範圍。
