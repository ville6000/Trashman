<template>
  <div class="px-6">
    <div class="flex flex-wrap my-6 -mx-2" v-if="collectionSpots.length > 0">
      <CollectionSpot
        v-for="collectionSpot in collectionSpots"
        :key="collectionSpot.spot_id"
        class="sm:w-1/2 my-2"
        :collectionSpot="collectionSpot"
      ></CollectionSpot>
    </div>
  </div>
</template>

<script>
import CollectionSpot from "./CollectionSpot.vue";

export default {
  name: "SearchResults",
  components: { CollectionSpot },
  props: ["collectionSpots"]
};
</script>