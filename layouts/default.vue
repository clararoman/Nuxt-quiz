<template>
  <b-container class="outer">
    <div id="header">
      <div class="logo"></div>
    </div>
    <nuxt />
  </b-container>
</template>

<script>
</script>

<style lang="scss">
html {
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen,
    Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
}

.outer {
  margin-top: 2em;
}
.logo {
  background-color: #e8e8e8;
  width: 2em;
  height: 2em;
}
</style>