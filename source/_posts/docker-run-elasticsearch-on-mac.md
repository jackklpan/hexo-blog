---
title: docker run elasticsearch on mac
tags:
  - docker
  - elasticsearch
date: 2015-12-27 20:57:00
---

First remember set up the config correctly.
Or you don't mount config folder in the first time and copy the config by command:

    docker cp &lt;containerId&gt;:/file/path/within/container /host/path/target

Run by this command:
docker run -d -p 9200:9200 -p 9300:9300 -v "$PWD/data":/usr/share/elasticsearch/data -v "$PWD/config":/usr/share/elasticsearch/config elasticsearch /bin/bash -c 'usermod -u 1000 elasticsearch; gosu elasticsearch elasticsearch'

From:
https://hub.docker.com/_/elasticsearch/

<div style="box-sizing: inherit; color: #555555; font-family: 'Helvetica Neue', Helvetica, Roboto, Arial, sans-serif; font-size: 16px; line-height: 1.6; margin-bottom: 1.25rem; padding: 0px; text-rendering: optimizelegibility;">Lots of people have complained about the AccessDenied issue. This usually occurs when using docker machine (or boot2docker) on a Mac. I previously got around this by running elasticsearch as root but you can't do that on the 2.x release.</div><div style="box-sizing: inherit; color: #555555; font-family: 'Helvetica Neue', Helvetica, Roboto, Arial, sans-serif; font-size: 16px; line-height: 1.6; margin-bottom: 1.25rem; padding: 0px; text-rendering: optimizelegibility;">My solution to this is based on the mount of /Users from the Mac into the boot2docker vm /Users is owned by the docker user who has uid 1000\. When you look at the mount of the folder from the vm into the container, you can see that the user is 1000 (no name since there is no user with uid of 1000 defined in the container).</div><div style="box-sizing: inherit; color: #555555; font-family: 'Helvetica Neue', Helvetica, Roboto, Arial, sans-serif; font-size: 16px; line-height: 1.6; margin-bottom: 1.25rem; padding: 0px; text-rendering: optimizelegibility;">The hack is to change the uid of the elasticsearch user to be 1000 and then he will have permission against any mounted volume from the Mac. Just use this is the command supplied to docker run</div><div style="box-sizing: inherit; color: #555555; font-family: 'Helvetica Neue', Helvetica, Roboto, Arial, sans-serif; font-size: 16px; line-height: 1.6; margin-bottom: 1.25rem; padding: 0px; text-rendering: optimizelegibility;">`/bin/bash -c 'usermod -u 1000 elasticsearch; gosu elasticsearch elasticsearch'`</div>