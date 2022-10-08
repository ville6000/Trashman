<template>
  <div class="w-full px-2">
    <div class="px-4 py-4 rounded overflow-hidden shadow-lg bg-white">
      <h2 class="font-bold text-gray-700 text-xl mb-2 leading-tight">{{ collectionSpot.name }}</h2>

      <p class="text-gray-600 text-base">
        {{ collectionSpot.address }}
        {{ collectionSpot.postal_code }}
        {{ collectionSpot.municipality }}
      </p>

      <div class="flex flex-wrap text-gray-700 mt-3">
        <div v-for="material in collectionSpot.materials" :key="material.code" class="mb-2 mr-2 text-sm p-1 bg-indigo-100">
          {{ material.name }}
        </div>

      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "SearchResults",
  props: ["collectionSpot"]
};
</script>