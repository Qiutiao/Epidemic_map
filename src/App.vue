<template>
  <div id="app">
    <Yee msg="Yeeeeee"/>
  </div>
</template>

<script>
import Yee from './components/疫情地图.vue'

export default {
  name: 'App',
  components: {
    Yee
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
