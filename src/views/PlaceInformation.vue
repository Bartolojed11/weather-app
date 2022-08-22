<script>
import { isProxy, toRaw } from "vue";
import moment from "moment";
import Error from '@/components/Error.vue'

export default {
  components: {
    Error
  },  
  data() {
    return {
      isReady: false,
      data: [],
      api_url: import.meta.env.VITE_API_URL,
      api_token: import.meta.env.VITE_API_TOKEN,
      headers: {},
      forecast: [],
      dates: [],
      selectedNdxForecast: 0,
      selectedForecast: [],
      showError: false
    };
  },
  async mounted() {
    this.headers = {
      Accept: "application/json",
      Authorization: `Bearer ${this.api_token}`,
      "Access-Control-Allow-Origin": "*",
    };

    this.getPlaceInfo();
  },
  methods: {
    showForecast: function (ndx) {
      this.selectedNdxForecast = ndx;
      this.selectedForecast = this.forecast[ndx];

      // if (isProxy(this.selectedForecast)) this.selectedForecast = toRaw(this.selectedForecast)
    },
    getPlaceInfo: async function () {
      const filter = this.setFilter();
      const response = await fetch(
        `${this.api_url}location/weather-forecast?${filter}`,
        {
          headers: this.headers,
        }
      );

      const data = await response.json();
      this.data = data;
      this.isReady = true;
      this.setDateAndTemp();

      if (this.data.status === 400) {
        this.showError = true
        setTimeout(() => {
        this.$router.push('/');
        }, 4000)
      }
    },
    setFilter: function () {
      let filter = "";
      Object.entries(this.$route.query).forEach((qry) => {
        filter += `&${qry[0]}=${qry[1]}`;
      });

      filter = filter.slice(1);
      return filter;
    },

    setDateAndTemp: function () {
      let list = this.data;
      let dates = [];
      let forecast = [];
      let pastDate = "";
      let presentDate = "";
      let temporaryData = {};
      let temporaryDateAndTemp = [];

      if (isProxy(list)) list = toRaw(list);

      list = list.data?.list || [];

      for (var i = 0; i < list.length; i++) {
        presentDate = moment(list[i].dt_txt).format("MMM DD");

        if (i == 0) {
          temporaryData = {
            icon: list[i].weather[0].icon || "",
            icon_description: list[i].weather[0].description || "",
            temp_max: list[i].main.temp_max || "",
            temp_min: list[i].main.temp_min || "",
            feels_like: list[i].main.feels_like || "",
            time: moment(list[i].dt_txt).format("hh:mm a"),
          };

          temporaryDateAndTemp.push(temporaryData);
          pastDate = presentDate;
          continue;
        }

        if (pastDate !== presentDate) {
          dates.push(presentDate);
          forecast.push(temporaryDateAndTemp);
          temporaryData = {};
          temporaryDateAndTemp = [];
        } else {
          temporaryData = {
            icon: list[i].weather[0].icon || "",
            icon_description: list[i].weather[0].description || "",
            temp_max: list[i].main.temp_max || "",
            temp_min: list[i].main.temp_min,
            feels_like: list[i].main.feels_like || "",
            time: moment(list[i].dt_txt).format("hh:mm a"),
          };

          temporaryDateAndTemp.push(temporaryData);
        }
        pastDate = presentDate;
      }

      this.dates = dates;
      this.forecast = forecast;
      this.selectedForecast = this.forecast[0] || [];
    },
  },
};
</script>

<template>
  <main>

    <Error :show="showError" />
    <div class="place-info-container" v-if="isReady && (data.status == 200)">
      <h1 class="heading-title letter-spacing-normal">
        {{ data.data.city.name }}
      </h1>
      <div class="place-info-coordinates">
        <span>Latitude : {{ this.$route.query.lat || "" }}</span>
        <span>Longitude : {{ this.$route.query.lon || "" }}</span>
      </div>

      <div class="date-select-container">
        <ul>
          <li v-for="(date, index) in dates" :key="index">
            <button
              type="button"
              class="button-crystal btn-data-select"
              :class="index === selectedNdxForecast ? 'active' : ''"
              @click="showForecast(index)"
            >
              {{ date }}
            </button>
          </li>
        </ul>
      </div>

      <section class="weather-information">
        <div class="weather-info-header odd flex">
          <p>Time</p>
          <p></p>
          <p>Condition</p>
          <p>High</p>
          <p>Low</p>
          <p>Precip</p>
        </div>

        <div class="weather-info-body">
          <div class="desktop">
            <div
              class="flex align-center"
              :class="index % 2 !== 0 ? 'odd' : ''"
              v-for="(fcast, index) in selectedForecast"
              :key="index"
            >
              <p>{{ fcast.time }}</p>
              <p class="txt-center">
                <img
                  class="forecast-icon"
                  :src="data.icon_url + fcast.icon + '.png'"
                  alt="weather url"
                />
              </p>
              <p>{{ fcast.icon_description }}</p>
              <p>{{ fcast.temp_max + " " + data.temp_symbol }}</p>
              <p>{{ fcast.temp_min + " " + data.temp_symbol }}</p>
              <p>{{ fcast.feels_like + " " + data.temp_symbol }}</p>
            </div>
          </div>

          <div class="mobile">
            <div class="flex just-between"
            :class="index % 2 !== 0 ? 'odd' : ''"
            v-for="(fcast, index) in selectedForecast"
              :key="index"
            >
              <div class="temp-left-content flex">
                <div class="temp-icon flex flex-xy-center">
                  <img
                    class="forecast-icon"
                    :src="data.icon_url + fcast.icon + '.png'"
                    alt="weather url"
                  />
                </div>
                <div class="flex flex-column just-center">
                  <p>{{ fcast.icon_description }}</p>
                  <p>{{ fcast.time }}</p>
                </div>
              </div>

              <div class="temp-right-content">
                <p>High: {{ fcast.temp_max + " " + data.temp_symbol }}</p>
                <p>Low: {{ fcast.temp_min + " " + data.temp_symbol }}</p>
                <p>Precip: {{ fcast.feels_like + " " + data.temp_symbol }}</p>
              </div>
            </div>
          </div>
        </div>
      </section>
    </div>
  </main>
</template>
