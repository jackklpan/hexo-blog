---
title: 'Maps with Leaflet, TopoJSON'
tags: []
date: 2014-11-18 23:42:00
---

A really good article that teach to use leaflet to show map. 
[http://blog.webkid.io/maps-with-leaflet-and-topojson/](http://blog.webkid.io/maps-with-leaflet-and-topojson/) 
Below is my note of this article 
<pre class="brush: html">
&lt;!DOCTYPE html&gt;  
&lt;html&gt;  
&lt;head&gt;  
  &lt;meta charset=&quot;UTF-8&quot;&gt;
  &lt;title&gt;maps with leaflet &amp; topojson&lt;/title&gt;
  &lt;link rel=&quot;stylesheet&quot; href=&quot;http://cdn.leafletjs.com/leaflet-0.7.3/leaflet.css&quot; /&gt;
  &lt;style&gt;
    html,body,#worldmap{
      height:100%;
    }
  &lt;/style&gt;
&lt;/head&gt;  
&lt;body&gt;  
  &lt;div id=&quot;worldmap&quot;&gt;&lt;/div&gt;  

  &lt;script src=&quot;http://cdn.leafletjs.com/leaflet-0.7.3/leaflet.js&quot;&gt;&lt;/script&gt;
  &lt;script&gt;
  // create a map object and set the view to the coordinates 24.875224031804528,121.53076171875 with a zoom of 9
  var map = L.map('worldmap').setView([24.875224031804528,121.53076171875], 9);
  &lt;/script&gt;
&lt;/body&gt;  
&lt;/html&gt;  
</pre>You will get a blank full screen leaflet map. (nothing show in the map) 
In leaflet [tutorial](http://leafletjs.com/examples/quick-start.html), their is a map with streets show up in background. 
<pre class="brush: javascript">
L.tileLayer('http://{s}.tiles.mapbox.com/v3/MapID/{z}/{x}/{y}.png', {
    attribution: 'Map data &copy; [OpenStreetMap](http://openstreetmap.org) contributors, [CC-BY-SA](http://creativecommons.org/licenses/by-sa/2.0/), Imagery © [Mapbox](http://mapbox.com)',
    maxZoom: 18
}).addTo(map);
</pre>This code in tutorial is the reason for it. It add a overlayer(openstreetmap) to map through a service called mapbox. 
But, in our case, we don't need this overlayer, just keep it blank first. And load a topoJson in next step.
<pre class="brush: html">
&lt;script src=&quot;http://d3js.org/topojson.v1.min.js&quot;&gt;&lt;/script&gt;  
&lt;script src=&quot;//code.jquery.com/jquery-1.11.0.min.js&quot;&gt;&lt;/script&gt;
</pre>Leaflet do not know about topoJson, so we need to convert it to geoJson in the browser. 
Use the code below to extend leaflet class. <pre class="brush: javascript">
L.TopoJSON = L.GeoJSON.extend({  
  addData: function(jsonData) {    
    if (jsonData.type === "Topology") {
      for (key in jsonData.objects) {
        geojson = topojson.feature(jsonData, jsonData.objects[key]);
        L.GeoJSON.prototype.addData.call(this, geojson);
      }
    }    
    else {
      L.GeoJSON.prototype.addData.call(this, jsonData);
    }
  }  
});
// Copyright (c) 2013 Ryan Clark
</pre>Then we can Load the data and set up some interactive function for each layer in topoJson. <pre class="brush: javascript">
var topoLayer = new L.TopoJSON();

$.getJSON('data/countries.topo.json')
  .done(addTopoData);

function addTopoData(topoData){  
  topoLayer.addData(topoData);
  topoLayer.addTo(map);
  topoLayer.eachLayer(handleLayer);
}

function handleLayer(layer){  
  layer.setStyle({
    fillColor : '#D5E3FF',
    fillOpacity: 1,
    color:'#555',
    weight:1,
    opacity:0.5
  });

  layer.on({
    mouseover: enterLayer,
    mouseout: leaveLayer
  });
}

function enterLayer(){  
  var countryName = this.feature.properties.name;
  //get the properties in topoJson
  console.log(countryName);

  this.bringToFront();
  this.setStyle({
    weight:2,
    opacity: 1
  });
}

function leaveLayer(){  
  this.bringToBack();
  this.setStyle({
    weight:1,
    opacity:.5
  });
}
</pre>