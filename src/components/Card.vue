<script>
import { RouterLink } from "vue-router";
// defineProps({
//   msg: {
//     type: String,
//     required: true,
//   },
// });
</script>
<template>
  <div class="card flex-1">
    <div class="card-content container-fluid">
      <h1 class="card-title font-highlight">Yokohama</h1>
      <div>
        <span>Latitude: </span>
        <span>138.2529</span>
      </div>

      <div>
        <span>Longitude: </span>
        <span>1.1111</span>
      </div>
      <div class="flex just-between mt-4px">
        <h1 class="card-small-title font-highlight">Today's weather forecast</h1>
      </div>

      <section class="card-weather-forecast">
        <div class="flex just-between wrap">
          <p>1:00 PM</p>
          <p>icon</p>
          <p>umuulan</p>
          <p>39C</p>
        </div>
        <div class="flex just-between wrap">
          <p>1:00 PM</p>
          <p>icon</p>
          <p>umuulan</p>
          <p>39C</p>
        </div>
      </section>
    </div>
    <div class="card--footer">
      <RouterLink to="/" class="btn-more-details">
        More details
      </RouterLink>
    </div>
    <!-- <button class="btn btn-primary btn-more-details">More details</button> -->
  </div>
</template>