<template>
  <div class="px-2">
    <div
      class="flex flex-wrap mt-4 pb-4 -mx-2 justify-left"
      v-if="collectionSpots.length > 0"
    >
      <CollectionSpot
        v-for="collectionSpot in collectionSpots"
        :key="collectionSpot.spot_id"
        class="max-w-sm rounded overflow-hidden shadow-lg w-full sm:w-1/2 md:w-1/3 lg:w-1/4 px-2 m-4 flex flex-col bg-white"
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

<style scoped>
</style>