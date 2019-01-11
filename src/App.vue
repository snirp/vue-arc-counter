<template>
  <div id="app">
    <ArcCounter width="10rem" height="10rem"></ArcCounter>
  </div>
</template>

<script>
import ArcCounter from '@/ArcCounter.vue'

export default {
  name: 'app',
  components: {
    ArcCounter
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
