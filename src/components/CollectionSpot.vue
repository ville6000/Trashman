<template>
  <div>
    <div class="px-6 py-4">
      <div class="font-bold text-gray-700 text-xl mb-2">
        {{ collectionSpot.name }}
      </div>
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