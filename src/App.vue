<template>
  <div id="app">
    <Reservas /> 
  </div>
</template>

<script>
import Reservas from "@/components/Reservas.vue"

export default {
  name: "App",
  components: {
    Reservas
  },
  
};
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@100&display=swap');
#app {
  max-width: 1000px;
  margin: 0 auto;
  text-align: center;
  font-family: 'Roboto', sans-serif;
}
</style>
