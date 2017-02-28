---
title: docker notes on mac
tags:
  - docker
date: 2015-12-27 21:05:00
---

List all containers:

    docker ps -a`</pre>
    Remover all stopped containers:
    <pre style="background-color: #eeeeee; border: 0px; color: #222426; font-family: Consolas, Menlo, Monaco, 'Lucida Console', 'Liberation Mono', 'DejaVu Sans Mono', 'Bitstream Vera Sans Mono', 'Courier New', monospace, sans-serif; font-size: 13px; margin-bottom: 1em; max-height: 600px; overflow: auto; padding: 5px; width: auto; word-wrap: normal;">`docker rm `docker ps -aq`

docker-machine ls

To Prevent the virtualbox machine use many memory

<div class="p1"><span class="s1">VBoxManage controlvm default poweroff</span></div><div class="p1"><span class="s1">after stop the docker</span></div>