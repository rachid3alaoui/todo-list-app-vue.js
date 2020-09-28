<template>
  <div id="app">
    <Home/>
  </div>
</template>

<script>
import Home from './components/Home.vue'

export default {
  name: 'App',
  components: {
    Home
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  background-image: linear-gradient(120deg, #f6d365, #fda085);
  color: white;
  font-family: "Ubuntu" , sans-serif;
  min-height: 100vh;
}
</style>
