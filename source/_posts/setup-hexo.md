---
title: 建置Hexo
tags: hexo
---
介紹參考了哪些網頁來建置Hexo，首先第一個當然是Hexo的[官方網站](https://hexo.io/zh-tw/)，根據官方網站可以有基本的設定，但官方的介面不太好看，所以第二步就是使用別人寫好的Theme。
<!-- more -->

我使用的是[NexT](http://theme-next.iissnan.com/getting-started.html)，該主題很貼心的提供了很多相關的設定說明，比如：[增加Tag](http://theme-next.iissnan.com/theme-settings.html#tags-page)、[增加DISQUS](http://theme-next.iissnan.com/third-party-services.html#disqus)、[增加MathJax](http://theme-next.iissnan.com/third-party-services.html#mathjax)。

增加DISQUS時若要在local預覽，到_config.yml將url更改成localhost:4000（[參考](http://www.codeblocq.com/2015/12/Add-Disqus-comments-in-Hexo/)）。

大致上設定完成之後，另外更改NexT的文字大小。在：
```
themes/next/source/css/_variable/custom.styl
```
可以修改相關的設定：
```
// 正文字體大小
$font-size-base = 18px

$font-size-headings-base = 28px

$table-font-size = 18px

// 代碼字體大小
$code-font-size = 17px

$btn-default-font-size = 18px

$logo-font-size = 24px

$subtitle-font-size = 17px

$read-more-font-size = 18px

$site-description-font-size = 18px

```

## Quick Start

### Create a new post

``` bash
$ hexo new "My New Post"
```

More info: [Writing](https://hexo.io/docs/writing.html)

### Run server

``` bash
$ hexo server
```

More info: [Server](https://hexo.io/docs/server.html)

### Generate static files

``` bash
$ hexo generate
```

More info: [Generating](https://hexo.io/docs/generating.html)

### Deploy to remote sites

``` bash
$ hexo deploy
```

More info: [Deployment](https://hexo.io/docs/deployment.html)
