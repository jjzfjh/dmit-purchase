# DMIT 購買教學：從註冊、選方案到付款一次走完，看懂 Pro／EB／T1 線路、計費週期與缺貨怎麼處理

第一次打開 DMIT 的下單頁，多數人卡住的不是付款，而是選項。同一個機房有三條線路，一條線路底下又從 TINY、Pocket、STARTER 一路排到 GIANT，價格從年付 36.9 美元跳到月付 800 多美元。還沒註冊，就先被自己勸退了。

這篇分成兩段：前面講「買哪個」——機房、線路、計費週期怎麼定；後面講「怎麼買」——註冊、下單、付款、開通。中間會補上新買家最容易吃虧的幾條規則，例如退款窗口多短、換 IP 什麼時候免費、為什麼官網首頁找不到便宜方案。

## 先決定三件事：機房、線路、計費週期

### 機房：洛杉磯、香港、東京

DMIT 的 KVM VPS 只放在三個地方，選機房本質上是在選「你和大陸使用者之間的物理距離」。

- **東京**：走優化線路時 ping 大約落在 50–90ms，是三個機房裡對大陸延遲最低的。
- **香港**：Premium 系列有第三方實測記錄顯示全國三網平均延遲約 43ms（電信 42ms、聯通 42ms、移動 46ms），代價是價格最高。
- **洛杉磯**：即使走 CN2 GIA，正常也要 150–180ms。非即時用途（建站、串流、下載）沒問題，VoIP 和遊戲就別為難它了。

### 線路：Pro／EB／T1 差在哪

這一步比選配置重要。同樣是 2 核 2G，Pro 和 T1 的價差可能到好幾倍，差別全在回程路由。

| 線路 | 路由特徵 | 適合誰 | 價格檔 |
| --- | --- | --- | --- |
| Premium（Pro） | 三網回程 CN2 GIA，自有骨幹加成 | 電信用戶、對延遲有硬要求 | 最高 |
| Eyeball（EB） | 三網 CMIN2／9929 等中國方向優化 | 移動、聯通用戶，預算優先 | 中 |
| Tier 1（T1） | 純國際 BGP，無大陸專項優化 | 國際業務、落地機、備份、CI/CD | 最低 |

還有一個常被忽略的差別在超量之後。Pro 和 EB 用完流量會限速到 4–10Mbps，基本只能勉強跑；T1 是限速但**不限流量**，依方案落在 50Mbps 到 1Gbps，這也是不少人拿 T1 當下載機或中轉機的原因。

### 計費週期：為什麼便宜方案沒有月付

DMIT 支援月付、季付、半年付、年付。週期越長單價越低，這點和其他商家一樣。真正要留意的是：**部分低配款的計費週期會被收緊**，例如 AN5 平台的 TINY 級方案，有時只開放季付以上，月付選項直接消失。能不能月付，看下單頁當下的選項最準。

同樣地，DMIT 的循環折扣碼（recurring）通常只認非月付，而且是針對特定產品線發放的，別看到一串代碼就亂貼。

## DMIT 購買教學：從註冊到下單的完整流程

先把付款工具準備好：**支付寶、微信支付、PayPal、信用卡**都能用。PayPal 帳號的個人資料最好先補齊，不然結帳到一半會被卡住。

**1. 註冊帳號。** 進官網後右上角可以切換介面語言到中文。註冊表單要填姓、名（用拼音，不要出現中文）、Email、密碼，勾人機驗證，然後把服務條款視窗捲到最底、等倒數結束才能按 Close，最後按 Create Your Account。

**2. 收驗證信。** 系統會寄一組驗證碼到你剛填的信箱，回到頁面填入並按 Confirm。

**3. 進入商店。** 驗證完成後會跳到用戶中心，這時你還沒有任何服務，點「No Products/Services Ordered, Order Now」就能進方案列表。**這裡有個很多人踩過的點：官網首頁看不到最低價的方案，一定要註冊登入後才看得到完整清單。** 找不到那個年付 36.9 美元的 T1，不是你眼殘。

**4. 挑方案。** 決定機房與線路後，選一個有庫存的配置按 Continue。DMIT 的貨動得很快，熱門的低配款常在補貨後幾分鐘內清空，看到有貨就別拖著比價。

**5. 設定計費週期、主機名稱、root 密碼、作業系統。** 作業系統清單清一色是 Linux 發行版，**DMIT 不提供 Windows**。如果你只會用 Windows 桌面，這台機器買回來第一件事是學 SSH。

**6. 附加配置。** 額外 IPv4、額外記憶體、額外系統碟都是**單獨收費**的，預設不勾就不會加錢。沒有特殊需求的話直接跳過。

**7. 進購物車。** 確認訂單總覽沒問題，按 Checkout。有優惠碼的話，在購物車的欄位輸入後按 Validate Code 驗證，價格會即時更新。順帶一提，DMIT 平時並沒有長期公開的優惠碼，折扣多半綁在節慶或補貨活動上，而且限制條件寫得很細（哪些產品線、哪些付款週期能用），過期的碼貼上去只會顯示無效。

**8. 付款。** 已經有帳號就登入，沒有就在這個頁面直接填個人資訊與密碼建立帳號。選好付款方式、勾同意條款，按完成訂購。

**9. 等開通。** 付款完成後服務會自動開通，通知信寄到你註冊的 Email。

**10. 下載 SSH 金鑰。** 進後台左側「服務」找到剛買的機器，首次進入會提示下載金鑰。**私鑰只能下載一次**，之後再點會變成「重新生成」，金鑰一換，原本設定好的連線就全部要重來。下載後解壓縮，`id_rsa.pem` 就是連線用的檔案，帳號填 `root`，密碼填你下單時設的那組。

想直接從下單頁開始的話，可以走這個入口：👉 [前往 DMIT 官方商店挑選方案](https://www.dmit.io/aff.php?aff=12046)

## 全方案價格對照

先講一個前提：DMIT 的貨架上長期同時掛著 **AS3（AMD EPYC 7003）、AN4（EPYC 9004）、AN5（EPYC 9005）** 幾代平台，同名方案在不同平台上的核心數與價格會不一樣，庫存也輪動得很快。下面的價格是整理時各方案常見的公開標價，實際下單以頁面顯示為準。

### 洛杉磯（LAX）

| 方案 | 規格 | 流量與埠 | AS3 月付 | AN5 月付 | 購買 |
| --- | --- | --- | --- | --- | --- |
| Premium · TINY | 1C／2GB／20GB | 1TB @1Gbps | $10.90 | $12.98 | [查看此方案](https://www.dmit.io/aff.php?aff=12046&pid=100) |
| Premium · Pocket | 2C／2GB／40GB | 1.5TB @4Gbps | $16.90 | $18.90 | [查看此方案](https://www.dmit.io/aff.php?aff=12046&pid=137) |
| Premium · STARTER | 2C／2GB／80GB | 3TB @10Gbps | $34.90 | $38.90 | [前往下單頁](https://www.dmit.io/aff.php?aff=12046) |
| Premium · MINI | 4C／4GB／80GB | 5TB @10Gbps | $62.90 | $76.90 | [前往下單頁](https://www.dmit.io/aff.php?aff=12046) |
| Premium · MICRO | 4C／4GB／160GB | 7TB @10Gbps | $87.90 | $99.90 | [前往下單頁](https://www.dmit.io/aff.php?aff=12046) |
| Premium · MEDIUM | 4C–6C／8GB／160GB | 14TB @10Gbps | $199.90 | $219.90 | [前往下單頁](https://www.dmit.io/aff.php?aff=12046) |
| Premium · LARGE | 8C／16GB／320GB | 25TB @10Gbps | — | $459.90 | [前往下單頁](https://www.dmit.io/aff.php?aff=12046) |
| Premium · GIANT | 8C／24GB／640GB | 50TB @10Gbps | — | $839.90 | [前往下單頁](https://www.dmit.io/aff.php?aff=12046) |
| Eyeball · TINY | 1C／2GB／20GB | 1.5TB @2Gbps | $10.90 | $12.98 | [查看此方案](https://www.dmit.io/aff.php?aff=12046&pid=189) |
| Eyeball · Pocket | 2C／2GB／40GB | 3TB @4Gbps | $16.90 | $18.90 | [查看此方案](https://www.dmit.io/aff.php?aff=12046&pid=190) |
| Eyeball · STARTER | 2C／2GB／80GB | 5TB @10Gbps | $34.90 | $38.90 | [前往下單頁](https://www.dmit.io/aff.php?aff=12046) |
| Eyeball · MINI | 4C／4GB／80GB | 10TB @10Gbps | $62.90 | $76.90 | [前往下單頁](https://www.dmit.io/aff.php?aff=12046) |
| Eyeball · MICRO | 4C／4GB／160GB | 14TB @10Gbps | $87.90 | — | [前往下單頁](https://www.dmit.io/aff.php?aff=12046) |
| Eyeball · MEDIUM | 6C／8GB／160GB | 30TB @10Gbps | $199.90 | — | [前往下單頁](https://www.dmit.io/aff.php?aff=12046) |
| Tier 1 · WEE | 1C／1GB／20GB | 1TB @4Gbps | $36.90／年 | — | [前往下單頁](https://www.dmit.io/aff.php?aff=12046) |
| Tier 1 · TINY | 1C／1GB／20GB | 2TB @4Gbps | $6.90 | — | [前往下單頁](https://www.dmit.io/aff.php?aff=12046) |
| Tier 1 · STARTER | 2C／2GB／40GB | 4TB @10Gbps | $12.90 | — | [前往下單頁](https://www.dmit.io/aff.php?aff=12046) |
| Tier 1 · MINI | 2C／4GB／80GB | 8TB @10Gbps | $21.90 | — | [前往下單頁](https://www.dmit.io/aff.php?aff=12046) |
| Tier 1 · MICRO | 4C／4GB／120GB | 16TB @10Gbps | $32.90 | — | [前往下單頁](https://www.dmit.io/aff.php?aff=12046) |
| Tier 1 · MEDIUM | 4C／8GB／160GB | 32TB @10Gbps | $49.90 | — | [前往下單頁](https://www.dmit.io/aff.php?aff=12046) |
| Tier 1 · LARGE | 8C／16GB／320GB | 64TB @10Gbps | $99.90 | — | [前往下單頁](https://www.dmit.io/aff.php?aff=12046) |
| Tier 1 · GIANT | 8C／24GB／640GB | 128TB @10Gbps | $199.90 | — | [前往下單頁](https://www.dmit.io/aff.php?aff=12046) |

洛杉磯的 T1 和 Pro 經常同時在架，價差擺在眼前：T1 TINY 月付 6.9 美元起，Pro TINY 要 12.98 美元。多付的錢買的是回程路由，不是硬體。

### 香港（HKG）

| 方案 | 規格 | 流量與埠 | 價格 | 購買 |
| --- | --- | --- | --- | --- |
| Premium · TINY | 1C／1GB／20GB | 500GB @1Gbps | $39.90／月 | [查看此方案](https://www.dmit.io/aff.php?aff=12046) |
| Premium · STARTER | 1C／2GB／40GB | 1TB @1Gbps | $79.90／月 | [前往下單頁](https://www.dmit.io/aff.php?aff=12046) |
| Premium · MINI | 2C／2GB／60GB | 1.5TB @1Gbps | $126.90／月 | [前往下單頁](https://www.dmit.io/aff.php?aff=12046) |
| Premium · MICRO | 2C／4GB／80GB | 2TB @1Gbps | $179.90／月 | [前往下單頁](https://www.dmit.io/aff.php?aff=12046) |
| Premium · MEDIUM | 4C／4GB／160GB | 2.5TB @1Gbps | $239.90／月 | [前往下單頁](https://www.dmit.io/aff.php?aff=12046) |
| Eyeball · TINY | 1C／1GB／20GB | 800GB @1Gbps | $39.90／月 | [前往下單頁](https://www.dmit.io/aff.php?aff=12046) |
| Eyeball · STARTER | 1C／2GB／40GB | 1.5TB @1Gbps | $79.90／月 | [前往下單頁](https://www.dmit.io/aff.php?aff=12046) |
| Eyeball · MINI | 2C／4GB／60GB | 2.2TB @1Gbps | $126.90／月 | [前往下單頁](https://www.dmit.io/aff.php?aff=12046) |
| Eyeball · MICRO | 4C／4GB／80GB | 3TB @1Gbps | $179.90／月 | [前往下單頁](https://www.dmit.io/aff.php?aff=12046) |
| Eyeball · MEDIUM | 4C／8GB／160GB | 4TB @1Gbps | $239.90／月 | [前往下單頁](https://www.dmit.io/aff.php?aff=12046) |
| Tier 1 · WEE | 1C／1GB／20GB | 1TB @4Gbps | $36.90／年 | [前往下單頁](https://www.dmit.io/aff.php?aff=12046) |
| Tier 1 · TINY | 1C／1GB／20GB | 2TB @4Gbps | $6.90／月 | [前往下單頁](https://www.dmit.io/aff.php?aff=12046) |
| Tier 1 · STARTER | 1C／2GB／40GB | 4TB @4Gbps | $12.90／月 | [前往下單頁](https://www.dmit.io/aff.php?aff=12046) |
| Tier 1 · MINI | 2C／2GB／60GB | 8TB @4Gbps | $21.90／月 | [前往下單頁](https://www.dmit.io/aff.php?aff=12046) |
| Tier 1 · MICRO | 4C／4GB／80GB | 16TB @4Gbps | $32.90／月 | [前往下單頁](https://www.dmit.io/aff.php?aff=12046) |
| Tier 1 · MEDIUM | 4C／8GB／160GB | 32TB @4Gbps | $49.90／月 | [前往下單頁](https://www.dmit.io/aff.php?aff=12046) |
| Tier 1 · LARGE | 8C／16GB／320GB | 64TB @4Gbps | $99.90／月 | [前往下單頁](https://www.dmit.io/aff.php?aff=12046) |
| Tier 1 · GIANT | 8C／24GB／640GB | 128TB @4Gbps | $199.90／月 | [前往下單頁](https://www.dmit.io/aff.php?aff=12046) |

香港 Premium 目前同時有 AS3 與 AN5 兩個平台，AN5 的 MINI 級大約從 $149.90／月起，配置比同名的 AS3 版本高。香港的 Pro 和 EB 最低配都是 39.9 美元／月，配置卻只有 1 核 1G，這條線的價格基本上是在買「距離」和「路由品質」。

### 東京（TYO）

| 方案 | 規格 | 流量與埠 | 價格 | 購買 |
| --- | --- | --- | --- | --- |
| Premium · TINY | 1C／1GB／20GB | 0.5TB @1Gbps | $21.90／月 | [前往下單頁](https://www.dmit.io/aff.php?aff=12046) |
| Premium · STARTER | 1C／2GB／40GB | 1TB @1Gbps | $39.90／月 | [前往下單頁](https://www.dmit.io/aff.php?aff=12046) |
| Premium · MINI | 2C／2GB／60GB | 2TB @1Gbps | $79.90／月 | [前往下單頁](https://www.dmit.io/aff.php?aff=12046) |
| Premium · MICRO | 4C／4GB／80GB | 4TB @1Gbps | $159.90／月 | [前往下單頁](https://www.dmit.io/aff.php?aff=12046) |
| Premium · MEDIUM | 4C／8GB／160GB | 5TB @1Gbps | $259.90／月 | [前往下單頁](https://www.dmit.io/aff.php?aff=12046) |
| Premium · LARGE | 8C／16GB／320GB | 8TB @1Gbps | $429.90／月 | [前往下單頁](https://www.dmit.io/aff.php?aff=12046) |
| Premium · GIANT | 8C／24GB／640GB | 15TB @1Gbps | $799.90／月 | [前往下單頁](https://www.dmit.io/aff.php?aff=12046) |
| Eyeball · TINY | 三網 CMI 回程 | — | $25.90／月起，多數時間缺貨 | [前往下單頁](https://www.dmit.io/aff.php?aff=12046) |
| Tier 1 · WEE | 1C／1GB／20GB | 1TB @4Gbps | $36.90／年 | [前往下單頁](https://www.dmit.io/aff.php?aff=12046) |
| Tier 1 · TINY | 1C／1GB／20GB | 2TB @4Gbps | $6.90／月 | [前往下單頁](https://www.dmit.io/aff.php?aff=12046) |
| Tier 1 · STARTER | 1C／2GB／40GB | 4TB @4Gbps | $12.90／月 | [前往下單頁](https://www.dmit.io/aff.php?aff=12046) |
| Tier 1 · MINI | 2C／2GB／60GB | 8TB @4Gbps | $21.90／月 | [前往下單頁](https://www.dmit.io/aff.php?aff=12046) |
| Tier 1 · MICRO | 4C／4GB／80GB | 16TB @4Gbps | $32.90／月 | [前往下單頁](https://www.dmit.io/aff.php?aff=12046) |
| Tier 1 · MEDIUM | 4C／8GB／160GB | 32TB @4Gbps | $49.90／月 | [前往下單頁](https://www.dmit.io/aff.php?aff=12046) |
| Tier 1 · LARGE | 8C／16GB／320GB | 64TB @4Gbps | $99.90／月 | [前往下單頁](https://www.dmit.io/aff.php?aff=12046) |
| Tier 1 · GIANT | 8C／24GB／640GB | 128TB @4Gbps | $199.90／月 | [前往下單頁](https://www.dmit.io/aff.php?aff=12046) |

東京 Pro 是最常售罄的一條產品線。低配的 TINY 和 STARTER 常常在補貨後幾分鐘內被清掉，想買通常得盯著補貨通知等。補貨時間沒有固定規律，但中國的幾個大促節點（雙十一、黑色星期五、春節前後）比較容易出現新庫存。

想一次看清楚三個機房目前的在售狀況，從這裡進最省事：👉 [查看 DMIT 全機房方案與庫存](https://www.dmit.io/aff.php?aff=12046)

## 三個容易吃虧的規則

> **退款窗口比你想的短。** 購買 3 天內、且機器已使用的流量不超過 30GB，可以全額退款（扣掉支付閘道收的手續費）。3 到 30 天之間只能按比例退，計算方式是「剩餘時間」和「剩餘流量」兩者取高。超過 30 天就沒得談了。另外，同一系列產品退過 3 次之後，帳號就會被拒絕退款。
>
> **換 IP 不是隨時免費。** Pro 和 EB 系列要同時滿足：實例購買滿 7 天、距離上次換 IP 滿 15 天、ICMP 和所有 TCP 埠都被封、服務剩餘有效期至少 7 天，才能免費換一次。條件不滿足就是 5 美元一次。T1 系列則只提供付費更換，而且兩次之間要隔 3 天。IP 是系統隨機分配，不能指定段或指定 IP。
>
> **新機 7 天內一定會收費。** 條款寫得很直白：7 天內下的新訂單、剩餘時間不足 7 天的服務，換 IP 一律收費。所以「先買一台測一下，被封了馬上換」這個做法行不通。

退款申請送出後實例會被關閉，資料不會保留。要退就別在上面放重要東西。

## 常見問題

**為什麼官網首頁找不到年付 36.9 美元的方案？**
因為低價方案不會掛在首頁，必須先註冊並登入，從用戶中心的商店入口進去才看得到完整清單。

**選中的方案顯示缺貨怎麼辦？**
三個做法：換同線路的其他配置、等補貨、或從後台左上角的 Create → Server 進去看全部在售方案——那裡才是完整的貨架，首頁和推薦位只露一部分。

**付款後多久能用？**
付款完成後服務會自動開通，通知信同時寄到你的註冊信箱。第一件事是去後台下載 SSH 私鑰，記得只能下載一次。

**能裝 Windows 嗎？**
不行。DMIT 只提供 Linux 發行版，如果方案裡有 Ubuntu 就直接選它，中文資料最多。

**有沒有長期有效的優惠碼？**
沒有。DMIT 平時不定時發折扣，多半綁定節慶或補貨活動，而且會指定產品線與付款週期。購物車的 Validate Code 欄位會直接告訴你能不能生效，不用自己猜。

**買錯機房可以換嗎？**
不行。機房是產品的一部分，換機房等於換產品，只能重新下單，原本那台按退款規則處理。

## 下單前最後確認

把這幾件事想清楚，整個購買流程大概五分鐘就能走完：你要的是大陸訪問速度還是國際頻寬（決定選 Pro／EB 還是 T1）、使用者主要在電信還是移動網路（決定 Pro 還是 EB）、延遲敏感還是不敏感（決定香港／東京還是洛杉磯）。剩下就是確認計費週期能不能選到你要的長度，然後照上面的步驟往下點。

DMIT 的定價不便宜，貴的地方全在路由和頻寬上，硬體規格反而不是它的賣點。如果只是想要一台便宜的大硬碟 VPS，這裡沒有你想要的東西；如果你的專案真的卡在晚高峰掉速或丟包，那多付的這筆錢通常花得下去。
