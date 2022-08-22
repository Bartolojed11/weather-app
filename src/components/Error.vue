<script>
export default {
    props: ['show']
}
</script>

<template>
  <div class="error-wrapper" v-if="show">
    <div class="error-overflow"></div>
    <div class="error-modal">
      <div class="error-message">No destination found!</div>
      <div class="error-description">
        Please input a valid location on the search address
      </div>
    </div>
  </div>
</template>