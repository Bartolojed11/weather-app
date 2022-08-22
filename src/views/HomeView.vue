<script>
import Banner from "@/components/Banner.vue";
import Card from "@/components/Card.vue";
import { RouterLink } from "vue-router";
import _ from "lodash";

export default {
  data() {
    return {
      api_url: import.meta.env.VITE_API_URL,
      api_token: import.meta.env.VITE_API_TOKEN,
      defaultLocations: [],
      defaultLocationsLoaded: false,
      headers: {},
      search: "",
      awaitingSearch: false,
      searchSuggestions: [],
      searchSuggestionLoaded: false,
      timeoutQuery: null,
    };
  },
  components: {
    Banner,
    Card,
  },
  async mounted() {
    this.headers = {
      Accept: "application/json",
      Authorization: `Bearer ${this.api_token}`,
      "Access-Control-Allow-Origin": "*",
    };
    await this.getDefaultLocations();
  },
  methods: {
    getDefaultLocations: async function () {
      const response = await fetch(`${this.api_url}location`, {
        headers: this.headers,
      });
      const data = await response.json();
      this.defaultLocations = data;
      this.defaultLocationsLoaded = true;
    },

    setViewLocationUrl: function (endpoint, lon, lat) {
      return `${endpoint}?lon=${lon}&lat=${lat}`;
    },

    fetchDestinations: async function () {
      const response = await fetch(
        `${this.api_url}location/search?text=${this.search}`,
        {
          headers: this.headers,
        }
      );
      const data = await response.json();
      this.searchSuggestions = data;
      this.searchSuggestionLoaded = true;
    },
  },
  watch: {
    search: function (val, oldVal) {

      if (val.trim() === "") {
        this.searchSuggestions = [];
        this.awaitingSearch = true;
      }

        if (!this.awaitingSearch || oldVal === '') {
          var self = this;
          var debounceFetch = _.debounce(function () {
            self.fetchDestinations();
            self.awaitingSearch = false;
          }, 2000);

          debounceFetch();
        }

      this.awaitingSearch = true;
    },
  },
};
</script>

<template>
  <main>
    <div class="banner-search-wrapper">
      <Banner />
      <div class="search_destination-wrapper">
        <div class="search-wrapper">
          <input
            class="
              form-input
              search-destination-input
              form-input-large
              autocomplete-container
            "
            placeholder="Check Japan Location"
            v-model="search"
          />
          <img
            class="search-destination-icon"
            src="../assets/search.png"
            alt="search icon"
          />

          <ul
            class="search-suggestions"
            v-if="searchSuggestionLoaded && search !== ''"
          >
            <div v-if="searchSuggestions.data !== undefined">
              <li
                v-for="(suggestion, index) in searchSuggestions.data"
                :key="index"
              >
                <RouterLink
                  :to="
                    setViewLocationUrl(
                      '/details',
                      suggestion.properties.lon,
                      suggestion.properties.lat
                    )
                  "
                  class="btn-suggestion form-input"
                  >{{ suggestion.properties.formatted }}</RouterLink
                >
              </li>
            </div>

            <li
              v-if="
                searchSuggestionLoaded &&
                (searchSuggestions.data === undefined ||
                  searchSuggestions.data?.length == 0)
              "
            >
              <a href="/" class="btn-suggestion form-input anchor-disabled"
                >No results found</a
              >
            </li>
          </ul>
        </div>
      </div>
    </div>

    <div class="container random-destinations__container">
      <h1 class="heading-title text-center">DEFAULT JAPAN DESTINATIONS</h1>
      <h2 class="text-center">
        Choose any destination to check for weather and place information
      </h2>

      <div class="random-destinations">
        <section class="wrap" v-if="defaultLocationsLoaded">
          <Card
            v-for="(location, index) in defaultLocations"
            :key="index"
            :data="location"
          />
        </section>
      </div>
    </div>
  </main>
</template>