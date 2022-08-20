<script setup>
import Banner from "@/components/Banner.vue";
import Card from "@/components/Card.vue";

function test() {
  console.log("test");
}
</script>

<template>
  <main>
    <div class="place-info-container">
      <h1 class="heading__title letter-spacing-normal">Yokohama</h1>
      <div class="place-info-coordinates">
        <span>Latitude : 1.1111</span>
        <span>Longitude : 1.1111</span>
      </div>

      <div class="date-select-container">
        <ul>
          <li>
            <button
              type="button"
              class="button-crystal btn-data-select active"
              @click="test"
            >
              Aug 24
            </button>
          </li>
          <li>
            <button type="button" class="button-crystal btn-data-select" @click="test">
              Aug 25
            </button>
          </li>
          <li>
            <button type="button" class="button-crystal btn-data-select" @click="test">
              Aug 26
            </button>
          </li>
          <li>
            <button type="button" class="button-crystal btn-data-select" @click="test">
              Aug 27
            </button>
          </li>
          <li>
            <button type="button" class="button-crystal btn-data-select" @click="test">
              Aug 28
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
            <div class="flex">
              <p>9:00</p>
              <p>icon</p>
              <p>Broken Clouds</p>
              <p>100</p>
              <p>99</p>
              <p>100</p>
            </div>
            <div class="odd flex">
              <p>9:00</p>
              <p>icon</p>
              <p>Broken Clouds</p>
              <p>100</p>
              <p>99</p>
              <p>100</p>
            </div>
          </div>

          <div class="mobile">
            <div class="flex just-between">
              <div class="temp-left-content flex">
                <div class="temp-icon flex flex-xy-center">
                  <p>icon</p>
                </div>
                <div class="flex flex-column just-center">
                  <p>Broken Clouds</p>
                  <p>9:00</p>
                </div>
              </div>

              <div class="temp-right-content">
                <p>High: 100</p>
                <p>Low: 99</p>
                <p>Precip: 100</p>
              </div>
            </div>

            <div class="flex just-between odd">
              <div class="temp-left-content flex">
                <div class="temp-icon flex flex-xy-center">
                  <p>icon</p>
                </div>
                <div class="flex flex-column just-center">
                  <p>Broken Clouds</p>
                  <p>9:00</p>
                </div>
              </div>

              <div class="temp-right-content">
                <p>High: 100</p>
                <p>Low: 99</p>
                <p>Precip: 100</p>
              </div>
            </div>
          </div>
        </div>
      </section>
    </div>
  </main>
</template>
