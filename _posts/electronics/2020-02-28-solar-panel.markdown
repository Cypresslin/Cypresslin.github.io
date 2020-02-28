---
layout: post
title:  "太陽能板與太陽能控制器"
subtitle: "市面上有不少中國製「假的」MPPT 控制器，購買前請注意"
categories: [electronics]
---

# 前言
買了張小的太陽能板來玩，本來是打算自己找各種模組來組一套充放電系統，不過仔細想想除了鉛酸電池之外大概還要加上這些模組：
  * 穩壓模組 - 把板子輸出調整成可以充鉛酸電池的電壓
  * 鉛酸電池充放保護模組 - 防止過充 / 過放
  * Buck 降壓模組 - 從電池或板子輸出 5V 給週邊設備使用

看了看這樣搞好像有點麻煩（懶），而且光是穩壓模組就有 Buck-Boost 跟 SEPIC 兩種可以選，還得加上隔離二極體（Blocking Diode）防止電流從電池倒灌進板子，如果是太陽能板陣列可能還得加上旁路二極體（Bypass Diode）。

想了想不然就直接買個太陽能控制器吧，大部分這類產品都可以充鉛酸電池，有的甚至可以充鋰電池，而且都會帶有 USB 輸出與一些過充過放、逆流保護。結果資料查一查發現太陽能控制器也有兩種不同的設計，PWM（脈衝寬度調變）與 MPPT（最大功率點追蹤）。實際在拍賣上逛一圈可以找到不少 PWM 或 MPPT 的產品，不過就算是那些標榜貨在台灣的賣家看起來貨源也是從中國進來的，不僅款式一樣連圖上的簡體字都懶得改！更有甚者還直接跟你說出貨天數要一週，擺明就是要做代購生意了XD。

在拍賣市場全新太陽能控制器 PWM 的最低含運費可以找到大概一個 125 左右，而 MPPT 的含運費居然不到 300 塊？這就讓人有點疑惑了，因為網路上查到的文章大多說後者比前者貴上好多倍。花了一兩天看了不少 Youtube 分析影片才知道原來有不少不誠實的中國廠商會標榜自己是 MPPT，但其實裡面根本就是個 PWM 控制器（或者 MPPT 只是個產品名稱而不是功能？太陽餅裡面沒有太陽的概念？）總之很瞎，雖然我只有一塊小板子大概是沒有必要用上 MPPT，但浪費了這麼多時間那就把這些假 MPPT 列一列吧！

# 太陽能控制器
在這先把找到關於這兩種控制器背景知識的筆記寫一下，下面的資料與範例來自於 [Choosing the right solar charge controller/regulator](https://www.solar4rvs.com.au/buying/buyer-guides/choosing-the-right-solar-charge-controller-regulat/) 一文。

## PWM（脈衝寬度調變，Pulse Width Modulation）
基本上可以把這種控制器想成是一種開關（通常是用 MOSFET 金氧半導體場效電晶體當作開關），它的電路會先把太陽能板的電壓降到比電池高一點，然後這個開關會依據電池的電量以不同的頻率開啟與關閉來讓板子為電池充電，在電池沒什麼電的時候幾乎是一直開著，等到充得差不多之後會降低開啟的時間這樣，這也就是所謂的 PWM，直到充滿至截止電壓之後停止充電或是切換為開啟時間更短的涓流充電（Float voltage，要注意的是鋰電池似乎不是很建議用涓流充電，涓流充電會更需要精密的調校以免把電池弄壞）。

這裡的「壓降」就是 MPPT 控制器最大的賣點了，假設一張太陽能板的規格是最大輸出電壓 18V，最大輸出電流為 5.0A，那麼在使用 PWM 的控制器時太陽能板的電壓會被往下拉成比鉛酸 12V 略高一點的 13V，雖然此時輸出電流可能會高一點但不會是等比例的變化，不同的板子會有不同的曲線，假設這裡輸出是 5.2A，那個原本板子可以有 18 * 5 = 90W 的功率，但實際被控制器用的只有 13 * 5.2 = 67.6W

## MPPT（最大功率點追蹤，Maximum Power Point Tracking）
這種控制器則是一種 DC-DC 變壓器，所謂的追蹤，就是因為不同板子有著不同的電壓電流曲線，它可以自動調整從板子那邊來的電壓讓板子可以達到最大輸出功率，以上面這個例子來說它就是直接拿板子輸出的 18 * 5 = 90W 的功率再利用 DC-DC 直流變壓把他轉換成電池充電用的電壓，當然在轉換中會有能量耗損，而板子本身也會受溫度、陰影等環境影響而沒辦法以理論最大功率輸出，不過與 PWM 控制器相比這種 MPPT 控制器效率還是高上一些（差異大概可以到 20% 左右）。

它與 PWM 控制器在硬體上的不同就是裡面會有一顆例如 CN3722 這種專門用來提供最大功率點追蹤功能的 IC，另外最顯著的差異就是它會因為有著 DC-DC 直流變壓的功能而有一顆很大顆的電感！只要拆開發現裡面沒有電感的就很有可能是假的。

## PWM / MPPT 控制器購買準則
如果你整個系統不大，或是不那麼在意轉換效率（或有預算考量）那就可以買 PWM 的控制器；而若你的系統很大，甚至可以考慮使用多個控制器建構分散式的 MPPT 系統，讓它可以對每一張板子個別進行最大功率點追蹤（因為在一組太陽能電池陣列中，可能會有幾塊因為日照不均而使發電效率不同）來最大化發電效率。

這個 Great Scott 在 Youtube 上的影片 [MPPT VS PWM || Solar Charge Controller](https://www.youtube.com/watch?v=C0VZTqwE4Ls) 很值得一看，裡面比較了 PWM / MPPT 控制器的效率以及價格差異。

## MPPT 控制器辨識準則
如果是買模組自己搞的話那就簡單啦，直接看板子上有沒有一顆大電感，而且板子上應該都會強調自己用的是哪一顆 IC，最好的範例就是 Adam Welch 在 Youtube 上的影片 [Cheap(est?) Lithium MPPT Solar Charge Controller CN3722 - 12v Solar Shed](https://www.youtube.com/watch?v=liYZ5pYOZDE) 中提到的那塊板子。

如果是控制器的話，若能拆開來看是最準確的（一樣是檢查裡面有沒有一大顆電感），或者是你可以在大晴天下拿三用電錶測量控制器的輸入電壓與電流，看輸入端電壓是不是會被往下拉到電池電壓附近（當然這也要你的板子輸出本來就高於電池電壓，像是 18V 這樣，可以參考上面 Great Scott 的影片）

但還沒購買時要怎麼判斷咧？大概有幾點可以參考：
  * 價格 - 太便宜的...大概沒啥好貨，多半是 PWM 型的然後上面印上 MPPT 字樣這樣（最可惡的就是假貨又賣很貴的XD）。
  * 標籤 - 如果它真的是 MPPT 型的，那麼機身上、盒子上、說明書上一定到處都會印上 MPPT 的字樣，沒有寫的高達 87 成不是，Adam Welch 的 Youtube 影片 [MPPT or PWM? Perfect Suitor Solar Charge Controller](https://www.youtube.com/watch?v=TfB_iIF-rCA) 中提到的 Perfect Suitor 的那款就是這樣，只有拍賣網站上有寫 MPPT 機身上卻沒有
  * 牌子 - 如果有廠牌的會比較保險一點
  * 善用搜尋，如果有看到某款控制器價差很大那就要注意囉，用 Fake MPPT 上網搜尋也會找到很多憤怒買家的分享XD

## 假的 MPPT 控制器
這裡列出幾個看到的幾款假 MPPT 控制器，節省大家的時間，看到這種就可以跳過了。

### 藍黑色機身，上有 MPPT SOLAR charge controller 字樣
![假MPPT - 藍黑色機身](/images/2020-02-fake-mppt/blue-black.jpg)
中國製品，拆開裡面根本沒有電感
Homemade 102 - [Inside MPPT battery charger CHINA](https://www.youtube.com/watch?v=TIAIr8fkYX4)

### 灰色機身，橘色字樣，上有 MPPT MXX 字樣（XX為數字）
![假MPPT - 灰色機身](/images/2020-02-fake-mppt/gray-orange.jpg)
中國製品，拆解與實測都在在顯示這不是 MPPT
Julian Ilett - [Review: MPPT-M20 Solar Charge Controller #1 - It's a Fake](https://www.youtube.com/watch?v=KA3X8XLxWHU)
Julian Ilett - [Review: MPPT-M20 Solar Charge Controller #2 - A Devious Fraud](https://www.youtube.com/watch?v=la-gvy0DfJs)

## 同場加映 - 便宜的 PWM 控制器
在看 Adam Welch 的影片時，發現他也有拆解了兩款很便宜的 PWM 控制器（大概就是拍賣上會看到一百多兩百塊的那款）：
[Anself CMTD 3S Lithium Solar Charge Controller - 12v Solar Shed](https://www.youtube.com/watch?v=I1hrWOP7WYA)
[Inside Another Cheap Solar Charge Controller](https://www.youtube.com/watch?v=9fjeYi3SwLc)
裡面安培數的不同看起來居然只是增加幾個 MOSFET，在功率不高的狀況下可能還好，但是如果是要架高瓦數的系統時可能要考慮一下這種適不適合你用。


# 參考資料
  * [Choosing the right solar charge controller/regulator](https://www.solar4rvs.com.au/buying/buyer-guides/choosing-the-right-solar-charge-controller-regulat/)
  * [Adam Welch's Youtube channel](https://www.youtube.com/channel/UCm5sG3-BXQZfVy3st2T_XKg)
