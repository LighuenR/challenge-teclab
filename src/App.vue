<template>
  <div id="app">
    <Formulario />
    <Timeline />
    <Tabla />
  </div>
</template>

<script>
import Formulario from "@/components/reservas/Formulario.vue";
import Tabla from "@/components/reservas/Tabla.vue";
import Timeline from "@/components/reservas/Timeline.vue";

export default {
  name: "App",
  components: {
    Formulario,
    Tabla,
    Timeline,
  },
};
</script>

<style>
</style>
