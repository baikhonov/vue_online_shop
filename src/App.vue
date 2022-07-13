<template>
  <div id="app">
    <v-main-wrapper></v-main-wrapper>
  </div>
</template>

<script>
import vMainWrapper from './components/v-main-wrapper'
import { mapActions, mapGetters } from 'vuex'

export default {
  name: 'App',
  components: {
    vMainWrapper
  },
  methods: {
    ...mapActions([
      'SET_MOBILE',
      'SET_DESKTOP',
    ]),
  },
  computed: {
    ...mapGetters([
      'IS_MOBILE',
      'IS_DESKTOP',
    ]),
  },
  mounted() {
    let vm = this
    window.addEventListener('resize', function() {
      if (window.innerWidth > 767) {
        vm.SET_DESKTOP()
        console.log('this is desktop')
      } else {
        vm.SET_MOBILE()
        console.log('this is mobile')
      }
    })
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
