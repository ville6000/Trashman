<template>
  <div class="map-container overflow-hidden bg-white" v-if="validCollectionSpots.length > 0">
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
        v-for="collectionSpot in validCollectionSpots"
        :key="collectionSpot.spot_id"
        :lat-lng="{lat: collectionSpot.geometry.coordinates[1], lng: collectionSpot.geometry.coordinates[0]}"
        :title="collectionSpot.name"
      >
        <l-popup>
          <h3 class="text-xl">{{ collectionSpot.name }}</h3>
          <p>{{ collectionSpot.address }}</p>
          <p v-html="collectionSpot.additional_details "></p>
          <p v-html="collectionSpot.opening_hours "></p>
        </l-popup>
      </l-marker>
    </l-map>
  </div>
</template>

<script>
import { LMap, LTileLayer, LMarker, LPopup } from "vue2-leaflet";
import { latLngBounds } from "leaflet";
import "leaflet/dist/leaflet.css";
import "leaflet-defaulticon-compatibility/dist/leaflet-defaulticon-compatibility.webpack.css"; // Re-uses images from ~leaflet package
import "leaflet-defaulticon-compatibility";

export default {
  name: "MapContainer",
  props: ["collectionSpots"],
  components: {
    LMap,
    LTileLayer,
    LMarker,
    LPopup
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
    },
    zoomToBounds() {
      if (
        this.validCollectionSpots.length === 0 ||
        typeof this.$refs.trashMap === "undefined"
      ) {
        return;
      }

      const bounds = latLngBounds();
      this.validCollectionSpots.forEach(spot => {
        bounds.extend({
          lat: spot.geometry.coordinates[1],
          lng: spot.geometry.coordinates[0]
        });
      });

      if (bounds.isValid()) {
        this.$refs.trashMap.mapObject.fitBounds(bounds);
      }
    }
  },
  computed: {
    validCollectionSpots: function() {
      const zeroPoint = 0.0;

      const spots = this.collectionSpots.filter(spot => {
        return (
          spot.geometry.coordinates[0] !== zeroPoint &&
          spot.geometry.coordinates[1] !== zeroPoint
        );
      });

      return spots;
    }
  },
  watch: {
    collectionSpots: function() {
      this.zoomToBounds();
    }
  },
  mounted() {
    this.zoomToBounds();
  }
};
</script>

<style scoped>
.map-container {
  height: 100vh;
}
</style>