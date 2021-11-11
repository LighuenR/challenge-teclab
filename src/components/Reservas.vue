!<template>
  <div>
    <Formulario @agregarReserva="agregarReserva($event)" />
    <Timeline :items="listaReservas" />
    <Tabla @eliminarReserva="eliminarReserva($event)" :items="listaReservas" />
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
      Tabla,
  },
  data() {
    return {
      listaReservas: [
        {
          id: 1,
          content: "Juan Perez",
          start: "2021-11-4 10:00",
          end: "2021-11-4 10:30",
          startTime: "10:00",
          endTime: "10:30",

        },
        {
          id: 2,
          content: "Juana Gonzalez",
          start: "2021-11-4 11:00",
          end: "2021-11-4 11:45",
          startTime: "11:00",
          endTime: "11:45",
        },
         {
          id: 3,
          content: "Leonardo Lupin",
          start: "2021-11-4 15:00",
          end: "2021-11-4 15:45",
          startTime: "11:00",
          endTime: "11:45",
        },
         {
          id: 4,
          content: "Sofia Allen",
          start: "2021-11-4 16:00",
          end: "2021-11-4 16:45",
          startTime: "11:00",
          endTime: "11:45",
        },
         {
          id: 5,
          content: "Susana Cañas",
          start: "2021-11-5 14:00",
          end: "2021-11-5 14:45",
          startTime: "11:00",
          endTime: "11:45",
        },
         {
          id: 6,
          content: "Ailen Rufino",
          start: "2021-11-6 11:00",
          end: "2021-11-6 11:45",
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
      },
      eliminarReserva(reserva){
          console.log(reserva)
          this.listaReservas.splice(
              this.listaReservas.indexOf(reserva), 1
          )
      }
  }
};
</script>

<style>


</style>