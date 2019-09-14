<template>
  <div
    class="mt-6 -mb-2 px-6 text-sm text-gray-600 text-base"
    v-if="resultCount"
  >Showing {{resultCount.results}} of {{resultCount.count}}</div>
</template>

<script>
export default {
  name: "ResultCount",
  props: ["resultCount"]
};
</script>