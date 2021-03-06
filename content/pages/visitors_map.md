Title: Visitors
Date: 2014-03-23 12:00
Author: cfarmer
Slug: maps/visitors
Icon: fa-map-marker
Status: hidden
Template: full_page

<link rel="stylesheet" href="http://cdn.leafletjs.com/leaflet-0.6.2/leaflet.css" />
<!--[if lte IE 8]><link rel="stylesheet" href="http://cdn.leafletjs.com/leaflet-0.6.2/leaflet.ie.css" /><![endif]-->
<script src="http://cdn.leafletjs.com/leaflet-0.6.2/leaflet.js"></script>
<link rel="stylesheet" href="../../libs/leaflet/MarkerCluster.css" />
<link rel="stylesheet" href="../../libs/leaflet/MarkerCluster.Default.css" />
<!--[if lte IE 8]><link rel="stylesheet" href="MarkerCluster.Default.ie.css" /><![endif]-->
<script src="../../libs/leaflet/leaflet.markercluster-src.js"></script>
<script src="../../libs/leaflet/leaflet-heat.js"></script>
<script type="text/javascript" src="http://maps.stamen.com/js/tile.stamen.js?v1.2.3"></script>
<script src="../../uploads/visitors_map.js"></script>

<div id="map"></div>
## <i class="fa fa-map-marker"></i> Recent visitors to carsonfarmer.com {.bold_title}

<script type="text/javascript">

    var layer = "toner";
    var loc = [34,-34, 3];
    var map = new L.Map("map", {
                    center: new L.LatLng(loc[0], loc[1]),
                    zoom: loc[2],
                    zoomControl: false
                });
    var stamen = new L.StamenTileLayer(layer, {opacity: 0.6});
    var heat = new L.heatLayer(visitors, {radius:40, max:4, maxZoom:2});
    var markers = L.markerClusterGroup({maxClusterRadius: 50, showCoverageOnHover: false});
    
    for (var i = 0; i < visitors.length; i++) {
        var a = visitors[i];
        var start = "Only "
        var end = " visitor..."
        if (a[3] > 1) {
            start = "At least ";
            end = " visitors!";
        }
        var place = a[2];
        var count = a[3];
        var title = start + count + end;
        var marker = L.marker(L.latLng(a[0], a[1]), {title: title});
        marker.bindPopup(place + "<br/>" + title);
        markers.addLayer(marker);
    }
    markers.bringToFront();
    map.addLayer(stamen);
    map.addLayer(markers);
    new L.Control.Zoom({ position: 'topright' }).addTo(map);
    L.control.layers(null, {'Clusters': markers, 'Heatmap': heat}).addTo(map);

</script>
