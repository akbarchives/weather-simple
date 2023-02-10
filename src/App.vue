<template>
  <Weather/>
</template>

<script>
import Weather from './components/Weather.vue'

import 'bootstrap/dist/css/bootstrap.css'
import 'bootstrap-icons/font/bootstrap-icons.css'


export default {
  name: 'App',
  components: {
    Weather,
  }
}
</script>

<style>
#app {
  /* font-family: Avenir, Helvetica, Arial, sans-serif; */
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /* text-align: center; */
  /* color: #2c3e50; */
  /* margin-top: 60px; */
}
</style>
