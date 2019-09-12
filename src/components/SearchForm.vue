<template>
  <div class="bg-white p-6 pt-4" @keyup.enter="doSearch">
    <div class="flex flex-wrap -mx-3 mb-4">
      <div class="w-full md:w-1/2 px-3">
        <label
          for="municipality"
          class="block uppercase tracking-wide text-gray-700 text-xs font-bold mb-2"
        >
          Municipality
        </label>
        <input
          type="text"
          name="municipality"
          id="municipality"
          class="appearance-none block w-full bg-gray-200 text-gray-700 border border-gray-200 rounded py-3 px-4 mb-3 leading-tight focus:outline-none focus:bg-white focus:border-gray-500"
          v-model="municipality"
        />
      </div>

      <div class="w-full md:w-1/2 px-3">
        <label
          for="postalCode"
          class="block uppercase tracking-wide text-gray-700 text-xs font-bold mb-2"
        >
          Postal Code
        </label>
        <input
          type="text"
          name="postalCode"
          id="postalCode"
          class="appearance-none block w-full bg-gray-200 text-gray-700 border border-gray-200 rounded py-3 px-4 mb-3 leading-tight focus:outline-none focus:bg-white focus:border-gray-500"
          v-model="postalCode"
        />
      </div>
    </div>
    <ul v-if="materialTypes.length > 0" class="flex flex-wrap my-2">
      <li
        v-for="materialType in materialTypes"
        :key="materialType.code"
        class="mr-4 mb-2"
      >
        <label
          class="block uppercase tracking-wide text-gray-700 text-xs font-bold mb-2 cursor-pointer"
        >
          <input
            type="checkbox"
            name="material"
            v-bind:value="materialType.code"
            v-model="material"
          />
          {{ materialType.name }}
        </label>
      </li>
    </ul>

    <button
      type="submit"
      class="bg-purple-500 hover:bg-purple-700 text-white uppercase font-semibold py-2 px-4 rounded outlin"
      @click="doSearch"
    >
      Search
    </button>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "SearchForm",
  data() {
    return {
      materialTypes: [],
      municipality: null,
      postalCode: null,
      material: []
    };
  },
  methods: {
    doSearch() {
      this.$emit("search", {
        municipality: this.municipality,
        postalCode: this.postalCode,
        material: this.material
      });
    }
  },
  mounted() {
    axios
      .get(
        `${process.env.VUE_APP_API_URL}/materialtypes/?api_key=${process.env.VUE_APP_API_KEY}`
      )
      .then(response => {
        this.materialTypes = response.data.results;
      });

    if (this.$route.query) {
      if (this.$route.query.material) {
        this.material = this.$route.query.material.split(",");
      }

      if (this.$route.query.municipality) {
        this.municipality = this.$route.query.municipality;
      }

      if (this.$route.query.postalCode) {
        this.postalCode = this.$route.query.postalCode;
      }
    }
  }
};
</script>