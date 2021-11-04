!<template>
  <div>
    <Formulario @agregarReserva="agregarReserva($event)" />
    <Timeline :items="listaReservas" />
    <Tabla :items="listaReservas" />
  </div>
</template>

<script>
import Formulario from "@/components/reservas/Formulario.vue";
import Timeline from "@/components/reservas/Timeline.vue";
import Tabla from "@/components/reservas/Tabla.vue";

export default {
  components: {
      Formulario,
      Timeline,
      Tabla
  },
  data() {
    return {
      listaReservas: [
        {
          id: 1,
          content: "Reserva 1",
          start: "2021-11-10 10:00",
          end: "2021-11-10 10:30",
          startTime: "10:00",
          endTime: "10:30",

        },
        {
          id: 2,
          content: "Reserva 2",
          start: "2021-11-9 11:00",
          end: "2021-11-9 11:45",
          startTime: "11:00",
          endTime: "11:45",
        },
      ],
    };
  },
  methods: {
      agregarReserva(reserva){
          console.log(reserva)
          this.listaReservas.push(reserva)
      }
  }
};
</script>

<style>


</style>