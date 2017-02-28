---
title: music rank player
tags:
  - front-end
  - side-project
date: 2016-10-02 14:47:00
---

製作
[https://jackklpan.github.io/music_rank_player/](https://jackklpan.github.io/music_rank_player/)

主要使用到以下東西
Lambda, Api Gateway, DynamoDB
vue.js
apex, (terraform)

Lambda串接googleapis和DynamoDB，查找歌曲在Youtube上面的播放Id，並存在DynamoDB，節省之後Youtube data api的查詢使用量。

Api Gateway串接Lambda，使前端可以用ajax query。

### Apex的雷：
googleapis裡面有資料夾相對路徑的結構，因此不能和apex github範例上一樣，用webpack全部合併成一個檔案，相對路徑會錯誤。
我直接在functions裡面的資料夾（和index.js同一層的地方），npm install googleapis，同一層會連同一起zip上去。

### Api Gateway的雷：
用terraform我覺得不好設定，直接用aws上面的介面比較容易。

在Method Request加上Query String

Integration Request加上Mapping，如下面網址說明，
使用application/json其中的預設template
[http://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-mapping-template-reference.html](http://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-mapping-template-reference.html)
但要修改escapeJavaScript，在兩個escapeJavaScript後面加上.replaceAll("\\'", "'")，如下面網址說明。否則當其中有 ' 符號的時候，會發生錯誤。
[https://forums.aws.amazon.com/thread.jspa?threadID=228917](https://forums.aws.amazon.com/thread.jspa?threadID=228917)

要加上CORS，使其他地方的domain也可以取用，如以下網址說明
[http://docs.aws.amazon.com/apigateway/latest/developerguide/how-to-cors.html](http://docs.aws.amazon.com/apigateway/latest/developerguide/how-to-cors.html)

### Youtube Api的雷：
<div>會有不能被embedded的影片，</div><div>用googleapis youtube api的時候加上videoEmbeddable: true可以濾掉一些。</div><div>不過有些影片是在某些domain才可以embedded的就無法濾掉了，所以這些影片會無法播放。</div><div>
</div>

### 其他的雷：
在Edge瀏覽器，要把script寫在一起才會Work...