<script setup>
import { RouterLink, RouterView } from 'vue-router'

defineProps({
  msg: {
    type: String,
    required: false
  }
})
</script>

<template>
  <nav class="navbar container">
    <RouterLink to="/">
      <img src="../assets/my-log.png" alt="JTRAVIN" />
    </RouterLink>
    <RouterLink to="/">HOME</RouterLink>
  </nav>
</template>

<style scoped>
  .navbar {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding-top: 1.6rem;
    padding-bottom: 1.6rem;
    box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25);
  }
</style>
