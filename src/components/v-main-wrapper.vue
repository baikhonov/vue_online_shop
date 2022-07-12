<template>
  <div class="v-main-wrapper">
    <div class="container">
      <keep-alive>
        <router-view></router-view>
      </keep-alive>
    </div>
  </div>
</template>

<script>

  export default {
    name: 'v-main-wrapper',
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
    max-width: 900px;
    margin: 0 auto;
  }
</style>