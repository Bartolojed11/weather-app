<script>
import { RouterLink } from "vue-router";
export default {
  props: ['data'],
  computed: {
    view_more_url() {
      return `/details?lon=${this.data.lon}&lat=${this.data.lat}`
    }
  }
}
</script>
<template>
  <div class="card flex-1">
    <div class="card-content container-fluid">
      <h1 class="card-title font-highlight">{{ data.city }}</h1>
      <div>
        <span>Latitude: </span>
        <span>{{ data.lat }}</span>
      </div>

      <div>
        <span>Longitude: </span>
        <span>{{ data.lon }}</span>
      </div>
      <div class="flex just-between mt-4px">
        <h1 class="card-small-title font-highlight">Today's weather forecast</h1>
      </div>

      <section class="card-weather-forecast">
        <div class="flex just-between align-center">
          <p><img :src="data.icon"/></p>
          <p>{{ data.weather_description }}</p>
          <p>{{ data.temp }}</p>
        </div>
      </section>
    </div>
    <div class="card--footer">
      <RouterLink :to="view_more_url" class="btn-more-details">
        More details
      </RouterLink>
    </div>
    <!-- <button class="btn btn-primary btn-more-details">More details</button> -->
  </div>
</template>