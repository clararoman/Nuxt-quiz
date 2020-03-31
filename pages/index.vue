<template>
  <b-container class="home">
    <b-row class="presentation">
      <b-col>Hello, I am Cloba Boba</b-col>
    </b-row>
    <b-row>
      <b-col class="column"></b-col>
    </b-row>
  </b-container>
</template>

<script>
export default {};
</script>

<style lang="scss" scoped>
.container {
  .home {
    margin-top: 2em;
  }
}
.column {
  background-color: #e8e8e8;
  height: 5em;
  &.column {
    margin-right: 1em;
  }
}
</style>
