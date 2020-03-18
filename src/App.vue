<template>
  <div id="app">
    <HomeComponent msg="COVID-19 Vue.Js"/>
  </div>
</template>

<script>
import HomeComponent from './components/HomeComponent.vue'


export default {
  name: 'App',
  components: {
    HomeComponent
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
  margin-top: 20px;
}
</style>
