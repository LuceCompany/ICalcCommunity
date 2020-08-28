<template>
  <div id="app">
    <ICalcCommunity />
  </div>
</template>

<script>
import ICalcCommunity from './components/ICalcCommunity.vue'

export default {
  name: 'App',
  components: {
    ICalcCommunity
  }
}
</script>

<style>
*{
  margin: 0px;
  padding: 0px;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
}
</style>
