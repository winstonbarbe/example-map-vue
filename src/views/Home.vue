<template>
  <div class="home">
    <div id="map"></div>
  </div>
</template>

<style>
#map {
  width: 500px;
  height: 500px;
}

#marker {
  background-image: url("https://upload.wikimedia.org/wikipedia/commons/7/7c/201408_cat.png");
  background-size: cover;
  width: 50px;
  height: 50px;
  border-radius: 50%;
  cursor: pointer;
}

.mapboxgl-popup {
  max-width: 200px;
}
</style>

<script>
// @ is an alias to /src
import mapboxgl from "mapbox-gl"; // or "const mapboxgl = require('mapbox-gl');"

export default {
  mounted: function() {
    // TO MAKE THE MAP APPEAR YOU MUST
    // ADD YOUR ACCESS TOKEN FROM
    // https://account.mapbox.com
    mapboxgl.accessToken = process.env.VUE_APP_MAPBOX_ACCESS_TOKEN;
    const map = new mapboxgl.Map({
      container: "map",
      style: "mapbox://styles/mapbox/streets-v11", // stylesheet location
      center: [-98.8438, 19.6925], // starting position [lng, lat]
      zoom: 14, // starting zoom
    });

    var popup = new mapboxgl.Popup({ offset: 25 }).setText(
      "This is a cat, on a pyramid"
    );

    // create DOM element for the marker
    var el = document.createElement("div");
    el.id = "marker";

    // create the marker
    new mapboxgl.Marker(el)
      .setLngLat([-98.8438, 19.6925])
      .setPopup(popup) // sets a popup on this marker
      .addTo(map);
  },
};
</script>
