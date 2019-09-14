<template>
  <div
    class="map-container overflow-hidden bg-white"
    v-if="collectionSpots.length > 0"
  >
    <l-map
      ref="trashMap"
      :zoom="zoom"
      :center="center"
      @update:zoom="zoomUpdated"
      @update:center="centerUpdated"
      @update:bounds="boundsUpdated"
    >
      <l-tile-layer :url="url"></l-tile-layer>

      <l-marker
        v-for="collectionSpot in collectionSpots"
        :key="collectionSpot.spot_id"
        :lat-lng="collectionSpot.geometry.coordinates"
      >
      </l-marker>
    </l-map>
  </div>
</template>

<script>
import { LMap, LTileLayer, LMarker } from "vue2-leaflet";
import { Icon } from "leaflet";
import "leaflet/dist/leaflet.css";

export default {
  name: "MapContainer",
  props: ["collectionSpots"],
  components: {
    LMap,
    LTileLayer,
    LMarker,
    Icon
  },
  data() {
    return {
      url: "https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png",
      zoom: 8,
      center: [63.096, 21.61577],
      bounds: null
    };
  },
  methods: {
    zoomUpdated(zoom) {
      this.zoom = zoom;
    },
    centerUpdated(center) {
      this.center = center;
    },
    boundsUpdated(bounds) {
      this.bounds = bounds;
    }
  }
};
</script>

<style scoped>
.map-container {
  height: 100vh;
}
</style>

