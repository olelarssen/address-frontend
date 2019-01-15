<template>
  <div id="app">
    <tip/>
  </div>
</template>

<script>
import Tip from './components/Tip.vue'

export default {
  name: 'app',
  components: {
    Tip
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
  width: 50%;
  margin: 0 auto;
  padding-top: 20%;
}
</style>
