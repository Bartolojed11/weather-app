<script setup>
import Banner from "@/components/Banner.vue";
import Card from "@/components/Card.vue";
</script>

<template>
  <main>
    <div class="banner-search__wrapper">
      <Banner />
      <div class="search_destination__wrapper">
        <div class="search-wrapper">
          <input
            class="form-input search-destination__input form-input-large"
            placeholder="Check Japan Location"
          />
          <img
            class="search-destination__icon"
            src="../assets/search.png"
            alt="search icon"
          />
        </div>
      </div>
    </div>

    <div class="container random-destinations__container">
      <h1 class="heading__title text-center">RANDOM JAPAN DESTINATIONS</h1>
      <h2 class="text-center">
        Choose any destination to check for weather and place information
      </h2>

      <div class="random-destinations">
        <section class="wrap">
          <Card />
          <Card />
          <Card />

          <Card />
          <Card />
          <Card />
        </section>
      </div>
    </div>
  </main>
</template>
