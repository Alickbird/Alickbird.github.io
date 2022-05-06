---
layout: default
---
[back](./dataviz_home)


<!-- Load Leaflet -->
<link rel="stylesheet" href="https://unpkg.com/leaflet@1.3.4/dist/leaflet.css" integrity="sha512-puBpdR0798OZvTTbP4A8Ix/l+A4dHDD0DGqYW6RQ+9jxkRFclaxxQb/SJAWZfWAkuyeQUytO7+7N4QKrDh+drA==" crossorigin=""/>
<script
  src="https://code.jquery.com/jquery-2.2.4.min.js"
  integrity="sha256-BbhdlvQf/xTY9gja0Dq3HiwQF8LaCRTXxZKRutelT44="
  crossorigin="anonymous"></script>
<script src="https://unpkg.com/leaflet@1.3.4/dist/leaflet.js" integrity="sha512-nMMmRyTVoLYqjP9hrbed9S+FzjZHW5gY1TWCHA5ckwXZBadntCNs8kEqAWdrb9O7rxbCaA4lKTIWjDXZxflOcA==" crossorigin=""></script>
<script src="https://unpkg.com/@turf/turf@3.5.2/turf.min.js"></script>

<!-- Create an element where the map will take place -->
<div id="mapid"></div>

<style>
#mapid { height: 400px; }
</style>

<script>
 
// Initialize the map
// mapid is the id of the div where the map will appear
var map = L.map('mapid',{
  center: [51.76, -1.25],
  zoom: 12
 });
  
var mylayer = L.layerGroup().addTo(map);
var bg = L.tileLayer(
    'https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
    attribution: 'Map data &copy; <a href="https://www.openstreetmap.org/">OpenStreetMap</a>'
    }).addTo(map);

  
//load GeoJSON from an external file
$.getJSON("https://raw.githubusercontent.com/Alickbird/Alickbird.github.io/main/oxfood.json", function( json ){
  L.geoJSON( json, {
    onEachFeature: addMyData,
  })
})
 
/*
function addMyData( feature, layer ){
  mylayer.addLayer(layer)
  // some other code can go here, like adding a popup with layer.bindPopup("Hello")
}
*/

function addMyData(feature,layer){
                        if (feature.geometry.type === 'Polygon') {
                            console.log('Polygon detected');
                            var centroid = turf.centroid(feature);
                            var lon = centroid.geometry.coordinates[0];
                            var lat = centroid.geometry.coordinates[1];
                            L.marker([lat,lon]).bindPopup(feature.properties.name).addTo(mylayer);
                        }
                        

}

var basemapControl = {
  "OSM Basemap": bg, // an option to select a basemap (makes more sense if you have multiple basemaps)
}
var layerControl = {
  "Pubs": mylayer, // an option to show or hide the layer you created from geojson
}

// Add the control component, a layer list with checkboxes for operational layers and radio buttons for basemaps
L.control.layers(basemapControl,layerControl ).addTo( map )

  
</script>
