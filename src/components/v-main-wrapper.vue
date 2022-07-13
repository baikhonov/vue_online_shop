<template>
  <div class="v-main-wrapper">
    <v-header></v-header>
    <div class="container">
      <keep-alive>
        <router-view></router-view>
      </keep-alive>
    </div>
  </div>
</template>

<script>
import vHeader from "./layouts/v-header"

  export default {
    name: 'v-main-wrapper',
    components: {
      vHeader
    },
    props: {

    },
    data() {
      return {
        title: 'Main wrapper'
      }
    },
    computed: {},
    methods: {},
    watch: {}
  }
</script>

<style>
  .container {
    padding: 0 15px;
  }

  .v-main-wrapper {
    margin: 100px 0 auto;
  }
</style>