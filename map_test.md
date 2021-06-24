---
layout: default
---

<!-- Load Leaflet -->
<link rel="stylesheet" href="https://unpkg.com/leaflet@1.3.4/dist/leaflet.css" integrity="sha512-puBpdR0798OZvTTbP4A8Ix/l+A4dHDD0DGqYW6RQ+9jxkRFclaxxQb/SJAWZfWAkuyeQUytO7+7N4QKrDh+drA==" crossorigin=""/>
<script src="jquery-2.1.1.min.js"></script>
<script src="https://unpkg.com/leaflet@1.3.4/dist/leaflet.js" integrity="sha512-nMMmRyTVoLYqjP9hrbed9S+FzjZHW5gY1TWCHA5ckwXZBadntCNs8kEqAWdrb9O7rxbCaA4lKTIWjDXZxflOcA==" crossorigin=""></script>

<!-- Create an element where the map will take place -->
<div id="mapid"></div>

<style>
#mapid { height: 400px; }
</style>

<script>

// Initialize the map
// mapid is the id of the div where the map will appear
var mymap = L
  .map('mapid')
  .setView([51.76, -1.25], 10);

// Add a tile to the map = a background. Comes from OpenStreetmap
L.tileLayer(
    'https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
    attribution: 'Map data &copy; <a href="https://www.openstreetmap.org/">OpenStreetMap</a>'
    }).addTo(mymap);
  
// load GeoJSON from an external file
$.getJSON("https://raw.githubusercontent.com/Alickbird/Alickbird.github.io/main/oxfood.json",function(data){
  // add GeoJSON layer to the map once the file is loaded
  L.geoJson(data).addTo(map);
  });


</script>

[back](./)
