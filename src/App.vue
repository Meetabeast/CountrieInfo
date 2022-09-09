<template>
  <my-countries></my-countries>
</template>

<script>
import myCountries from './components/countries.vue'

export default {
  name: 'App',
  components: {
    myCountries
  }
}
</script>

<style>
body {
  background-color: #111217;
  color: rgb(255, 255, 255);
  font-family: 'Poppins', sans-serif;
}
</style>
