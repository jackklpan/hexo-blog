---
title: 建置Hexo
tags: hexo
date: 2016-03-08 08:00:00
---
## 初始設定
Hexo的[官方網站](https://hexo.io/zh-tw/)，根據官方網站可以有基本的設定，但官方的介面不太好看，所以接下來要使用別人寫好的Theme。
<!-- more -->

使用的是[NexT](http://theme-next.iissnan.com/getting-started.html)，該主題很貼心的提供了很多相關的設定說明，比如：[增加Tag](http://theme-next.iissnan.com/theme-settings.html#tags-page)、[增加DISQUS](http://theme-next.iissnan.com/third-party-services.html#disqus)、[增加MathJax](http://theme-next.iissnan.com/third-party-services.html#mathjax)。

### NexT
這邊需要注意的是，因為之後要用到travis自動化deploy。NexT為獨立的git repo，若無特殊設定，並不會將其檔案下載下來，導致travis的自動化部署失敗（找不到theme檔案）。有兩種方法：

1.
```
rm themes/next/.gitignore
rm -r themes/next/.git
```
將NexT的git刪除，使其全部使用同一個git repo

2.
先fork NexT，並在此repo客製化後，將此repo視為submodule（請使用https的連結，避免權限問題）：
```
git submodule add https://your/custom/repo
```
之後於travis指令執行
```
git submodule init
git submodule update
```
即可以載入主題檔案。

### MathJax使用方法
```
$$ Block $$

\\(inline\\)
```

### DISQUS
增加DISQUS時若要在local預覽，到_config.yml將url更改成localhost:4000（[參考](http://www.codeblocq.com/2015/12/Add-Disqus-comments-in-Hexo/)）。

### NexT文字大小
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

## 匯入Blogger的文章

只能用RSS
``` bash
npm install hexo-migrator-rss --save
```

匯入
``` bash
hexo migrate rss "http://annotationandnote.blogspot.com/feeds/posts/default?alt=rss&max-results=1000000"
```

遇到個問題
``` bash
unknown block tag: load
```

是文章中有個
```
{% load %}
```
這種東西，將其包在code block即可。

## 部署到Github

我使用的方式是用repo的gh-pages。

```
npm install hexo-deployer-git --save
```

_config.yml：
```
deploy:
  type: git
  repo: git@github.com:xxx/xxx.git
  branch: gh-pages
```

```
url: https://xxx.github.io/xxx/
root: /xxx/
```

command：
```
hexo g
hexo deploy
```

## 使用Travis自動部署

參考Hexo作者的[文章](https://zespia.tw/blog/2015/01/21/continuous-deployment-to-github-with-travis/)

``` yml
language: node_js
node_js:
  - node
before_install:
  # Decrypt the private key
  - openssl aes-256-cbc -K $xxx_key -iv $xxx_iv
    -in .travis/xxx.enc -out ~/.ssh/id_rsa
    -d
  # Set the permission of the key
  - chmod 600 ~/.ssh/id_rsa
  # Start SSH agent
  - eval $(ssh-agent)
  # Add the private key to the system
  - ssh-add ~/.ssh/id_rsa
  # Copy SSH config
  - cp .travis/ssh_config ~/.ssh/config
  # Set Git config
  - git config --global user.name "jackklpan"
  - git config --global user.email jackklpan@gmail.com
  # Install Hexo
  - npm install hexo -g
  # Clone the repository, 產生的檔案會放置於.deploy_git，將其clone下來使commit一致，避免git force update
  - git clone --branch gh-pages https://github.com/jackklpan/hexo-blog.git .deploy_git
script:
  - git submodule init # 用于更新主题，需要指定到自己的repo，否则会clone最新NexT主题，客製化的部分會消失
  - git submodule update
  - hexo generate
  - hexo deploy
branches:
  only:
    - master
```
