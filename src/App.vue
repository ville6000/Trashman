<template>
  <div id="app" class="flex flex-wrap">
    <div class="h-full md:w-1/2">
      <AppHeader></AppHeader>
      <SearchForm v-on:search="search"></SearchForm>
      <ResultCount :resultCount="resultCount"></ResultCount>
      <SearchResults :collectionSpots="collectionSpots"></SearchResults>
    </div>
    <MapContainer :collectionSpots="collectionSpots" class="md:w-1/2"></MapContainer>
  </div>
</template>

<script>
import axios from "axios";
import AppHeader from "./components/AppHeader";
import SearchForm from "./components/SearchForm";
import ResultCount from "./components/ResultCount";
import SearchResults from "./components/SearchResults";
import MapContainer from "./components/MapContainer";

export default {
  name: "app",
  components: {
    AppHeader,
    SearchForm,
    ResultCount,
    SearchResults,
    MapContainer
  },
  data() {
    return {
      collectionSpots: [],
      resultCount: {
        count: 0,
        results: 0
      }
    };
  },
  methods: {
    search(params) {
      const query = {};

      if (params.municipality) {
        query["municipality"] = params.municipality;
      }

      if (params.postalCode) {
        query["postal_code"] = params.postalCode;
      }

      if (params.material && params.material.length > 0) {
        query["material"] = params.material.join(",");
      }

      this.$router.push({ path: "/", query }, () => {}, () => {});
      this.doSearch(params.municipality, params.postalCode, params.material);
    },
    doSearch() {
      const query = this.$route.query;
      const params = Object.keys(query)
        .map(function(k) {
          return encodeURIComponent(k) + "=" + encodeURIComponent(query[k]);
        })
        .join("&");

      axios
        .get(
          `${process.env.VUE_APP_API_URL}/collectionspots/?api_key=${process.env.VUE_APP_API_KEY}&${params}`
        )
        .then(response => {
          this.collectionSpots = response.data.results;
          this.resultCount.results = response.data.results.length;
          this.resultCount.count = response.data.count;
        });
    }
  },
  mounted() {
    if (this.$route.query) {
      this.doSearch();
    }
  }
};
</script>

<style>
body {
  @apply bg-gray-200;
}
</style>
