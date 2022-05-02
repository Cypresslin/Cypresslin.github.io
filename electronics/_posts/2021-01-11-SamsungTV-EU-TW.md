---
title:  "在台灣用 Samsung 的 220V 歐規電視？"
subtitle: "一台歐洲製造掛著歐洲規格的三星電視要怎才能在台灣用？"
categories: [electronics]
---

# 前言
本文沒什麼技術內容，單純就是筆記而已。

因緣際會踢到一台三星的智慧電視 UE40D6100SKXXU，高興之餘發現機殼上的標籤寫著輸入電壓 220V，嗯...看來要把他直接拿來用並不是那麼簡單的一件事！於是乎就開始了一段查找資料的奇幻旅程。

![電視標籤](/images/2021-01-SamsungTV/Label.jpg)

上網查了一下 Spec，這台 2011 年的機器畫質也有個 Full HD 1080p，而且居然可以有可以連有線網路、無線網路（需要搭配他們自己的 Linkstick Wifi USB）還有 3D 功能（也是一樣需要搭配他們的主動式 3D 眼鏡，不過可惜的是 3D 電視的發展大概在 2017 年就劃下了句點）不過看起來猴塞雷啊！

英國官網：https://www.samsung.com/uk/support/model/UE40D6100SKXXU/

# 測試
這台電視封存也好幾年了，當然是得先確定一下它到底還能不能用。剛好手邊也有 220V 的插座可以接，就直接給它上電開機試試：
![過電測試畫面與聲音](/images/2021-01-SamsungTV/PowerOn.jpg)

搭啦～可以用，HDMI 輸入跟聲音也都 OK！

# 電壓問題
好啦，既然確定 220V 可以正常開機，那麼想要在國內用這台歐規的電視基本上就幾個辦法：
  1. 直接接 220V 插座，家裡的冷氣插座會是 220V 的，所以只要用冷氣插座就可以搞定了，這只要確定插頭可以用就 OK，因為有的 220V 插座會刻意把其中一支腳轉 90 度讓使用者不容易搞混。另外就是台電近期也在推廣 220V 的市電，所以有些新一點的房子會有多的 220V 的插座可以用。再不然...就是要找水電師傅來弄一個插座。
  2. 買個 110V > 220V 的升壓轉換器，一個台灣製造的 300W 雙向轉換器大概在七百元左右，以這台 130W 的功耗來講完全是綽綽有餘。

比較奇特的是在官網以及使用者手冊上我都找不大到他的功耗以及輸入電壓等資訊，反而是在 [icecat 這個網站](https://icecat.biz/en/p/samsung/ue40d6100skxxu/tvs-ue40d6100-8917813.html)上找到的。

## 可不可以把電源板換成 110V 的？
此時突然也有個想法：**是不是有機會可以把裡面的電源板直接換成可以吃 110V 輸入的板子呢？**
根據之前拆其他電視的經驗，110V 的市電還是要經過電源板轉換成 LED 背光用的高壓輸出以及主機板用的 5V 待機電壓 / 12V，既然電源版本身就會有這種變壓功能，那如果找得到吃 110V 的板子理論上是可以無痛換上去的，不大可能歐規的電視吃 220V 但待機電壓變成兩倍的 10V 吧？這樣的話裡面的所有零件跟電路設計可能都要改。

而且反正如果真的找得到的話裝上去之前可以先比較一下 110V 的板子與 220V 板子各腳位的電壓，不要盲接大概都不用擔心把電視弄壞。

## 三星電視型號的命名規則
用 UE40D6100SK 這個型號在台灣的網站上找怎麼也找不到這台電視，原來是因為三星電視的命名規則限制了我的搜尋結果

如果以這串型號來解釋的話就是：
  * U - 代表 LED 電視，其他可能出現的是 Q = QLED、P = Plasma、L = LCD、H = DLP、K = OLED
  * E - 代表歐洲規格，亞洲是 A 而北美是 N
  * 40 - 電視的尺吋，這一台是 40 吋電視
  * D6100 - 電視的主、副系列碼，所以應該可以說這台是 6000 系列的 6100 型...吧，前面這個 D 似乎也代表了 2011 年的意思，不過因為我看官網上也是寫 D6100 我就沒把他拆開了
  * S - Twin Satellite Tuner（衛星調諧器，這應該跟要接衛星天線有關？）
  * K - 這一碼我還真的不知道是什麼，網路上也沒找
  * X - 特定買家碼，X 代表無特定標示（None）
  * XU - 販售國碼，XU 為英國，這個代碼除了表示它是適用於該國之外，也是表示保固只有在那裡有效

後面 SKXXU 這幾碼也代表了這台電視在英國以外的地方使用可能會影響訊號的接收以及智慧程式的使用，不過現在都嘛是接 HDMI 所以好像也沒差。

參考資料：
  * [Samsung UK - What do Samsung TV model numbers actually mean? Why are they so long?](https://www.samsung.com/uk/support/tv-audio-video/what-do-samsung-tv-model-numbers-actually-mean-why-are-they-so-long/)
  * [TAB-TV - Country Code in Samsung TV Model Number](https://en.tab-tv.com/?p=18100)
  * [alphr - Samsung TV Model Numbers Explained](https://www.alphr.com/technology/1007706/samsung-tv-model-numbers-explained/)

## 搜尋相容電源板
有了命名規則之後就可以來找看看其他地區有沒有類似型號的機器了不過很可惜的用 UAD6100 或是 UND6100 去找沒有，但是 D6000 在美國與台灣三星網站上可以找到這幾台不同大小的機器：
  * [UA32D6000SMXZW](https://www.samsung.com/tw/support/model/UA32D6000SMXZW/)
  * [UA40D6000SMXZW](https://www.samsung.com/tw/support/model/UA40D6000SMXZW/)
  * [UA46D6000SMXZW](https://www.samsung.com/tw/support/model/UA46D6000SMXZW/)
  * [UA55D6000SMXZW](https://www.samsung.com/tw/support/model/UA55D6000SMXZW/)

不確定裡面的板子到底會不會一樣，那就先從確定的東西下手 - 來找找 UED6100 的電源板吧！

用 UED6100 Power Board 去找會看到一張叫做 BN44-00458B (PD46A1D_BHS) 的電源板，用這個型號繼續找下去就可以發現一件有趣的事：
  1. 這個板子有個相近的型號 BN44-00458A (PD46A1D_BSM) ，網路上寫可以互通。從照片上來看兩張板子的 layout 不大一樣，但是通往主機板與背光板的排線插座位置是一樣的，真的要確定兩者能否通用的話就得去比較板子上所載明的各個接腳的定義與電壓一不一樣。
  2. 台灣的網拍上找不大到 BN44-00458B 的拆機零件，不過倒是買得到 BN44-00458A，而且後者適用的機型就是亞洲地區買得到的 UA40D6000 這台電視

這就有趣了，如果 BN44-00458B = BN44-00458A，而且 BN44-00458A 就是我們這邊標著輸入電壓 100 - 240V 電視所用的電源板的話那是不是代表其實寫著輸入 220V 的歐洲規格電視其實也是能吃 110V 呢？

繼續找了一些文章找到這一篇：[My Automated Palace - Are Samsung Smart TVs Dual Voltage? Helpful lessons](https://myautomatedpalace.com/are-samsung-smart-tvs-dual-voltage/) 其實網路上有蠻多類似的問題，結論大概就是三星絕大部分的電視都支援 100 - 240V 輸入（在成本上來說也比較合理），但是保險起見拆開來看電源板上的標示是最準的了。

## 拆解
查資料查到這其實心裡也有底了，反正也沒保固了拆開檢查看看也無妨。

**注意：電視內部有高壓迴路，在處理有 HOT 標示的區域請千萬要小心 Do this at your own RISK**

拆解就跟一般電視一樣，背後大大小小螺絲都拆掉就可以把背蓋拿下來了，螺絲有兩種規格，電視邊邊的都是用長的，短的用在背蓋內側：
![螺絲](/images/2021-01-SamsungTV/Screws.jpg)

拆掉背蓋後照片中黃色那塊就是這次要研究的主角 - 電源板（BN44-00458B）
![拆除背蓋後](/images/2021-01-SamsungTV/TearDown.jpg)

果不其然，板子上寫著 Input rating 100 ~ 240V，帥啊老皮！
![輸入電壓標記](/images/2021-01-SamsungTV/InputRating.jpg)

到這其實就可以安心的把他裝回去然後隨便找插座來接了，不過基於對人類的不信任以及可以殺死好幾隻貓的好奇心（反正拆了都拆了），我決定把線都拔掉來量一下各個腳位的輸出電壓，就算輸入電壓真的標示有誤也只是燒電源板～
![電源板各腳位輸出值](/images/2021-01-SamsungTV/OutputValue.jpg)

照表格上的值來看基本上就是背光高壓區有 5V / 5.3V / 12.8V / 253V 這幾種值，而輸出到主板的編號 CNM803 接頭則是有 5V / 5.3V / 12.8V 這幾種值。這次就先測 CNM803 這個接頭，比較奇怪的是在過電後沒接其他線的狀況下，12V 跟 5.3V 接腳量出來的電壓會從 0~12V 這樣跳動，5V 輸出則是很穩定的 5V。一開始還想說是不是壞了，直到接上 220V 測試發現也有一樣的情況才安心，看來是有什麼 feedback 迴路在主板上（？），總之，接上主板看有待機電源燈之後就可以安心的把背光電源線也接回去然後開機測試了。

用 110V 開機也沒問題！關於電源的研究就到此一段落。

更詳細的拆解步驟與診斷可以在 ElektroTanya 這個網站上找到[維修手冊](https://elektrotanya.com/samsung_ue32d6100_ue32d6200_ue40d6000_ue40d6200_ue40d6100s_ue40d6200t_ue40d6300_chassis_u68a.pdf/download.html)

# 腳架
拿到這台電視時是沒有腳架的狀態，所以也在各大網拍上找了一下，最簡單的不外乎就是：
1. 相同機型拆機品
2. 通用腳架

相同機型的拆機品是最直覺的解決方案，不過這台在台灣沒有賣，要在國內找到對應的拆機品有點困難，從國外買的話運費加上去實在是很不划算XD。通用腳架則是鎖在背後 VESA 規格的孔上（也就是壁掛架的鎖孔）。

## 同一個原廠腳架有沒有可能用在不同型號的機器上？
出於好奇所以查了一下會不會有一個腳架適用於不同機型的可能性，這台電視的腳架看起來至少分成兩個部份，一個是鎖在機器上的部份 (Assembly Guide P-Stand)，一個是底座 (P-Base)，所以如果找得到一樣的 P-Stand 可以鎖上機器那就應該沒問題了！

用這台的型號加上 stand 為關鍵字查到了國外網友賣的拆機品，那個賣家很專業的附上了零件編號的近照，上面寫著：
UD6000 37"
GUIDE STAND
BN61-07057X

看來這個 BN61-07057X 就是我們要的 P-Stand 型號了，在 ebay 上拿這型號去 ebay 找可以找到有賣家說它適用於 37" 40" 46" D/ES 系列的電視：

![BN61-07057X 相容型號](/images/2021-01-SamsungTV/BN61-07057X-list.png)
來自 ebay 賣家的相容型號表

不過如果拿這個型號去美國的 [SamsungParts](http://www.samsungparts.com/) 官方授權的零件經銷商網站找是找不到的（也許又是歐洲型號跟其他地方的差異？），但倒是有一個相近的型號：[BN61-07057A](http://www.samsungparts.com/Products/Parts_and_Accessories/PID-BN61-07057A.aspx)，從列表上看同樣主要也是適用於 40 - 55 吋 D/ES 等系列的電視。歐洲也有一個 samsungparts.eu 網站，但不知道為什麼我的搜尋都無效），感覺最保險的作法還是實際看到零件編號再下手。

拍賣上是可以看到一些可能相容的拆機品，不過大部分的賣家都不會特別寫零件編號所以找起來也很麻煩。也許最「保值」的辦法大概就是去買通用型腳架了，萬一哪天這台機器退休了還可以把腳架拿去別的機器上用。

# 連網功能
這種很 fancy 的智慧電視最大的特點就是可以連上網，系統裡面有提供一些 App 可以讓你直接在電視上看網路節目。而這台電視只有有線網路可以用，並沒有內建無線網卡，如果想要用無線網路功能就得去買他們自家出的 Wifi dongle 來接，根據使用者手冊可以用的 USB 無線網卡為：
>To connect wirelessly, you must ﬁrst attach a “Samsung Wireless LAN Adapter” (WIS09ABGN, WIS09ABGN2, WIS10ABGN - sold separately) to either the USB 1 (HDD), USB 2 or USB 3 on the back of your TV.

不過我還是隨手拿了兩個其他牌子的 USB Wifi 網路卡來用，結果當然是不能用XD

這原因大概是因為主機裡面只有內建他們家出的網卡的驅動程式，我猜也許拿由其他廠商製造但晶片相同的網卡搞不好也可以用？一查果然有網友實驗過了XD（請見：[Mobile01 - Samsung的USB wireless: WIS09ABGN](https://www.mobile01.com/topicdetail.php?f=347&t=1727659)），以下為晶片列表以及網友分享的替代型號：

| Samsung Model | Chipset                | Replacement                          |
|---------------|------------------------|--------------------------------------|
| WIS09ABGN     | Ralink RT2870 + RT2850 | D-Link DWA-160 RevB / ZyXEL NWD-211AN|
| WIS09ABGN2    | Ralink RT3572          | Linksys WUSB600N Rev2                |
| WIS10ABGN     | Ralink RT3572          | Same as above                        |

不過實際測試就留待未來有機會拿到這些 USB 網卡再說吧，反正有線網路可以用（而且沒啥 app 好用的）～

# Netflix / YouTube 等 app
連上網後系統自動更新了不少東西，其中也包含了 Netflix 的 App。滿懷期待的開起來發現畫面會黑一下然後跳回主畫面，怎麼開都開不起來。我想可能是 App 太舊了吧...

上網查了一下，果不其然三星在 2019 的一篇公告指出因為一些「技術限制」，Netflix 在 2019 十二月二日之後將停止支援舊款的智慧電視，官網很賊的沒有列出受影響的型號，反倒是要大家自己去 Netflix 官網看支援裝置列表，我是在電視上沒看到這個訊息啦（難到舊到連官方訊息都沒有了嗎，哈），不過以這台這麼古老的年紀來說我想應該也是凶多吉少XD，而三星自己的討論區上也是哀鴻遍野。

而 YouTube 的部份電視上是已經看不到 app 了，大概是播放器從 Flash 轉換到 HTML5 而導致很多舊機器不再支援 Youtube 影片的播放。

應用程式下載中心裡還看得到華視新聞以及壹電視的 app，不過這兩者在顯示中文字元上有點問題，有些字會變成方塊，八成跟歐洲電視與字集的支援脫不了關係。

到這個人覺得電視這種壽命動輒十來年的東西好像還是買最簡單可以吃 HDMI 等影音輸入的就好XD，畢竟這麼久的時間難保廠商會願意給你一直更新下去。而且在家家戶戶可能都會裝 mod 等機上盒的狀況下這些 app 就有點雞肋，真的想要比較厲害的功能倒不如去買一台 Chromecast 或者是裝上 [Kodi](https://kodi.tv/) 的 RaspberryPi 來用。

參考資料：[Samsung - A message appears on your TV: Netflix will no longer be available on this device](https://www.samsung.com/us/support/troubleshooting/TSG01203568/)
