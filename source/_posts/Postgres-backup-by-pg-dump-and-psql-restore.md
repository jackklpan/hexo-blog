---
title: Postgres backup by pg_dump and psql restore
tags:
  - postgresql
  - sql
date: 2015-02-05 21:43:00
---

pg_dump --data-only -t "\"MixedCaseName\"" &gt; xxx.txt
(add -o if you want to retain id)

Use psql to delete all data from the table.

sudo sudo -u username psql -U username -d dbname -f filename(xxx.txt)