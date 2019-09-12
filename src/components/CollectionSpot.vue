<template>
  <div class="px-2">
    <div class="w-full px-4 py-4 rounded overflow-hidden shadow-lg bg-white">
      <h2 class="font-bold text-gray-700 text-xl mb-2 leading-tight">
        {{ collectionSpot.name }}
      </h2>

      <p class="text-gray-600 text-base">
        {{ collectionSpot.address }}
        {{ collectionSpot.postal_code }}
        {{ collectionSpot.municipality }}
      </p>
    </div>
  </div>
</template>

<script>
export default {
  name: "SearchResults",
  props: ["collectionSpot"]
};
</script>

<style scoped>
</style>