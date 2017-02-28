---
title: ST_GeomFromGeoJSON connection terminated & crash
tags:
  - postgis
  - postgresql
  - sql
date: 2015-04-27 22:49:00
---

The postgis function&nbsp;ST_GeomFromGeoJSON &nbsp;sometimes cause database crash.
[http://dba.stackexchange.com/questions/83264/st-geomfromgeojson-causes-postgres-to-crash](http://dba.stackexchange.com/questions/83264/st-geomfromgeojson-causes-postgres-to-crash)
[http://trac.osgeo.org/postgis/ticket/3002](http://trac.osgeo.org/postgis/ticket/3002)

And I cannot find any solution for it.

Therefore, I do it workaround.
I convert the geojson to kml and then use ST_GeomFromKML.
[https://github.com/mapbox/tokml](https://github.com/mapbox/tokml)
<pre class="brush: javascript">var kml = tokml(geojson.geometry);
//left only the geometry part
kml = kml.replace('&lt;?xml version="1.0" encoding="UTF-8"?&gt;&lt;kml xmlns="http://www.opengis.net/kml/2.2"&gt;&lt;Document&gt;&lt;Placemark&gt;&lt;ExtendedData&gt;&lt;/ExtendedData&gt;', "").replace("&lt;/Placemark&gt;&lt;/Document&gt;&lt;/kml&gt;", "");
</pre><div>
</div>