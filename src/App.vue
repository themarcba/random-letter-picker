<template>
  <div id="app">
    <RandomLetter></RandomLetter>
  </div>
</template>

<script>
import RandomLetter from './components/RandomLetter.vue'

export default {
  name: 'app',
  components: {
    RandomLetter
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
