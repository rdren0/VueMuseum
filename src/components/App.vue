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
  text-align: center;
  color: #2c3e50;

}
body{
  background-image: url("https://images.pexels.com/photos/984541/pexels-photo-984541.jpeg?auto=compress&cs=tinysrgb&dpr=2&h=750&w=1260");
  background-size: contain;
}

</style>
