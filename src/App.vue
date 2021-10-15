<template>
  <Home></Home>
</template>
<script>
import Home from './components/Home.vue';

export default {
  components:{
    Home,
  }
};
</script>

<style lang="scss">
*{
  margin: 0;
  padding: 0;
}
body{
  background-color: cornflowerblue;
  font-size: 14px;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

</style>
