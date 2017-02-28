---
title: sql + postgresql + postgis usage
tags:
  - postgis
  - postgresql
  - sql
date: 2015-04-25 22:45:00
---

[http://www.w3schools.com/sql/default.asp](http://www.w3schools.com/sql/default.asp)

prevent sql injection:
[http://fecbob.pixnet.net/blog/post/39095519-%E9%A0%90%E9%98%B2sql%E6%B3%A8%E5%85%A5%E6%94%BB%E6%93%8A](http://fecbob.pixnet.net/blog/post/39095519-%E9%A0%90%E9%98%B2sql%E6%B3%A8%E5%85%A5%E6%94%BB%E6%93%8A)
In summary:
1\. Use&nbsp;Parameterized Query
2\. Data validation for integer and date...etc.
3\. Replace the ' to '' ( Replace("'", "''") ) for string type.
4\. Use ‎appropriate user role to connect database.

POSTGIS:
[http://revenant.ca/www/postgis/workshop/indexing.html](http://revenant.ca/www/postgis/workshop/indexing.html)
[http://workshops.boundlessgeo.com/postgis-intro/](http://workshops.boundlessgeo.com/postgis-intro/)

ST_GeomFromGeoJSON =&gt; connection terminated, because this function cause database crash!
[http://dba.stackexchange.com/questions/83264/st-geomfromgeojson-causes-postgres-to-crash](http://dba.stackexchange.com/questions/83264/st-geomfromgeojson-causes-postgres-to-crash)
and I cannot find any solution to this.

優化與維護:
[https://ruimemo.wordpress.com/2010/03/31/postgresql-performance-and-maintenance-%EF%BC%88postgres-%E4%BC%98%E5%8C%96%E4%B8%8E%E7%BB%B4%E6%8A%A4/](https://ruimemo.wordpress.com/2010/03/31/postgresql-performance-and-maintenance-%EF%BC%88postgres-%E4%BC%98%E5%8C%96%E4%B8%8E%E7%BB%B4%E6%8A%A4/)

VACUUM ANALYZE&nbsp;CLUSTER

DB size:
SELECT pg_size_pretty(pg_database_size('dbname'));

Table size:
SELECT&nbsp;pg_size_pretty(pg_total_relation_size('cities_region'));

Top 10 size:
SELECT relname AS "relation", pg_size_pretty(pg_relation_size(C.oid)) AS "size"
&nbsp; FROM pg_class C LEFT JOIN pg_namespace N ON (N.oid = C.relnamespace)
&nbsp; WHERE nspname NOT IN ('pg_catalog', 'information_schema')
&nbsp; ORDER BY pg_relation_size(C.oid) DESC
&nbsp; LIMIT 10;