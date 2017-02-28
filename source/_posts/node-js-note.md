---
title: node.js note
tags:
  - node.js
date: 2015-05-13 19:43:00
---

Production:
forever
pm2

From Tonyq([https://www.facebook.com/tonylovejava/posts/10206912577918652?fref=nf](https://www.facebook.com/tonylovejava/posts/10206912577918652?fref=nf))
* package.json 是專案設定檔，可以用來設定 dependency (會用到哪些 npm ，分成專案用跟開發用兩種 dependency / dev-dependency）。

有設定的話剛 clone 別人專案回來時，可以用 "npm install" 直接安裝專案相依性到 local 。好處是不用把 node_modules commit 進版本控制，降低大小跟環境依賴。

* npm init 是如果沒有 package.json 可以用這個快速產生一個。

* npm install &lt;package&gt; //正常的安裝套件流程

如果沒有指定 package 的話，會自動安裝 package.json 裡面的相依性.

但如果你是裝專案需要的 npm package 的話，可以加上 "--save" ，如 npm install &lt;package&gt; --save ，會順便更新 package.json 檔加入這個 dependency。

如果你是給 gulp 或其他開發工具用的，可以用 --save-dev ，會寫入 dev-dependency 區。

另外跟這個沒有直接關係，但值得知道的事情是 "-g" 屬性，有支援 npm install -g &lt;package&gt; 的 npm ，會把該 package 直接變成 global 的 command。像是 express /browserify 等等等。(windows 底下這個功能有點 buggy ...)

==
發現我漏講了 npm run
在 package.json 裡面有 scripts properties 。可以在裡面直接寫入你要執行的 "command line"(!!) 指令

像是我手上這專案是這樣
"scripts": {
"test": "echo \"Error: no test specified\" &amp;&amp; exit 1",
"dev": "supervisor --extensions 'node,js,jsx' app.js"
},

就可以透過 npm run dev 來執行「supervisor --extensions 'node,js,jsx' app.js」

npm install &lt;package&gt; 如果不帶上 --save 或 --save-dev 的話，所安裝的 package 將不會自動記進 package.json。

但是，這些模塊仍會安裝在你的 node_modules。這時候你可以透過 npm prune 命令，清除這些不在 package.json 裡的模塊。

這有時候在調試時，這還滿好用的。

PS: bower prune 也有同樣功能。

-----

From 陳樂子 in ([https://www.facebook.com/groups/javascript.tw/permalink/628502737251068/](https://www.facebook.com/groups/javascript.tw/permalink/628502737251068/))
npm install &lt;package&gt; -g 即是 --global，會把你的模塊裝到全局裡去，只要是在這個 node 環境下，所有項目都會共用著這些模塊，例如 npm gulp bower mocha 通常都是這樣使用。

你 npm install mocha -g，安裝完成後，你便可以直接在任何地方執行 mocha --check-leaks --reporter spec 之類的命令。

若你不想每次都要污染全局，你依然可以僅安裝在本地項目目錄上，只是若你要調試的話，便變成在要給模塊指定一個路徑，例如 node_modules/mocha/bin/mocha --check-leaks --reporter spec。

你也可以透過 package.json 的 scripts 預先來編好一些腳本，再透過 npm run &lt;command&gt; 來執行。透過 npm run 執行的腳本，所有安裝在本地的模塊，皆不再須要幫它編寫路徑。

因此你可以直接這樣作

$ npm install npm-dep-info

// package.json
"scripts": {
"info": "npm-dep-info"
}

$ npm run info

-----

附帶一提，我命令都是用縮寫比較快。

例如

- npm i 取代 npm install

- npm un 取代 npm uninstall

- npm i -S 取代 npm install --save

- npm i -D 取代 npm install --save-dev