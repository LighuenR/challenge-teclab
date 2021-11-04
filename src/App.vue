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
#app {
  max-width: 1200px;
  margin: 0 auto;
  text-align: center;
}
</style>
