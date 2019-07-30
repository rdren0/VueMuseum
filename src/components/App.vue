<template>
  <div id="app">
    <Header />
    <Container/>
  </div>
</template>

<script>
import Header from "./Header.vue";
import Container from './Container.vue'

export default { 
  name: "app",
  components: {
    Header,
    Container
  },  
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

</style>
