---
title: iOS Missing IOS Distrubution signing identity
tags:
  - ios
date: 2016-02-21 20:26:00
---

From: 
https://dotblogs.com.tw/aken1215/2016/02/15/234033

<div class="article__content">                    <div class="article__desc">                        憑證顯示"<span style="color: red;">無效的簽發者</span>"
                        </div>搞了三小時才找到問題，問題的病徵其實很詭異，就當今天一如往常的想要將開發好的 APP發佈新版本，一切都很順利，一直到要輸出成ipa檔的時候，系統提示"<span style="color: red;">Missing IOS Distrubution &nbsp;signing&nbsp;identity &nbsp;for...</span>"的錯誤．身為一個在IOS世界裡打滾一小陣子的開發人員，很直覺得就會猜

1.  該不會又是該死的certificate過期了吧？可是回想一下，年初才全部更新過呀，全部都沒過期
2.  該不會又是certificate的私鑰找不到？於是就打開Key Chan，看到憑證和私鑰都存在．
3.  不合邏輯啊！該不會是provision profile選錯certificate？於是又重新從apple developer網頁下載provision profile 安裝完還是不行
4.  還是不行OOXX，心想，檢查一下Xcode的Target=&gt;General=&gt;Bundle identifier吧，還是沒錯....
5.  快沒招了，最後檢查XCode的Target =&gt; BuildSetting =&gt;Code&nbsp;Signing ，還是沒錯....我暈....以上講了五個步驟，其實都跟本篇的解決方案無關，但這次真的是例外，上面五個步驟，在遇到類似這種錯誤訊息通常都是可以順利解決的．而這次，這些步 驟我至少重複玩了一小時，甚至還從頭到尾 建立CSR=&gt;申請certificate=&gt;建立provision  profile=&gt;下載安裝certificate=&gt;下載安裝provision profile  =&gt;設定xocde全部跑過一次，還是無法解決．直到點開Key Chan裡的憑證，看到左下角有一個紅色叉叉寫著"<span style="color: red;">無效的簽發者</span>"才大致找到問題源頭，不看還好，一看心臟快停止，全部至少10多張憑證在同一時間全部都顯示這個訊息．不得已只好膜拜google大神...
  [https://developer.apple.com/support/certificates/expiration/](https://developer.apple.com/support/certificates/expiration/)&nbsp;=&gt;  apple 的解釋，大致上是說有一個叫做"The Apple Worldwide Developer Relations  Certification Intermediate  Certificate"的簽發人憑證即將在2016/2/14到期(謎之聲：不知道是apple裡的那位工程師不爽看大家在情人節放閃，故意在情人節要 捅大家)，不過文章也有說，你不需要重新產生所有已存在的憑證，原本可以運作的APP也都會正常運作．大致重點就這樣．不過他是說你在運行的APP不會掛 掉，但可沒說你要是想發布新版本APP卻沒更新該憑證就會中招．
  那要怎麼做呢？

1.  [https://developer.apple.com/certificationauthority/AppleWWDRCA.cer](https://developer.apple.com/certificationauthority/AppleWWDRCA.cer)=&gt;下載新版憑證&nbsp;
2.  將下載的憑證連續點兩下即可安裝
3.  打開Key Chan=&gt;顯示方式=&gt;顯示已過期憑證 =&gt;在登入和系統的分類裡各有一張過期的憑證請把它刪除(謎之聲：沒刪除它不會套用你剛安裝的新憑證，這裏我又卡了半小時有吧，無言....）
4.  請檢查所有IOS憑證是否顯示綠色圈圈搭配"此憑證是有效的"訊息，如果有的話，恭喜，大功告成..&nbsp;</div>