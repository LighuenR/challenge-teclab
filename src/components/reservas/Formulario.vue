<template>
  <div class="card">
    <h2>RESERVAR</h2>
    <form ref="reservas" @submit.prevent>
      <input class="mx-input" style="max-width: 250px" type="text" placeholder="Nombre" v-model="content" />
      <date-picker placeholder="Fecha"  type="date" v-model="startDate" format="YYYY-MM-DD"></date-picker>
      <vue-timepicker close-on-complete placeholder="Hora de entrada" :minute-interval="15" v-model="startTime" format="HH:mm"></vue-timepicker>
      <vue-timepicker close-on-complete placeholder="Hora de salida" :minute-interval="15" v-model="endTime" format="HH:mm"></vue-timepicker>
      <button
        @click="
         agregarReserva( 
              {
            content: content,
            date: startDate.toISOString().split('T')[0],
            start: startDate.toISOString().split('T')[0] + ' ' + startTime,
            end: startDate.toISOString().split('T')[0] + ' ' + endTime,
            startTime,
            endTime
          })
        "
        class="mx-input"
      >
        Guardar
      </button>
    </form>
  </div>
</template>

<script>
import DatePicker from "vue2-datepicker";
import "vue2-datepicker/index.css";

import VueTimepicker from "vue2-timepicker";
import "vue2-timepicker/dist/VueTimepicker.css";

export default {
  components: { DatePicker, VueTimepicker },
  data() {
    return {
      startDate: "",
      content: "",
      startTime: "",
      endTime: "",
    };
  },
  methods: {
      agregarReserva(reserva) {
          this.$emit('agregarReserva', reserva)
          this.$refs.reservas.reset()
      }
  }

  
};
</script>

<style  scoped>
.card {
  padding: 2rem;
  margin: 2rem 0;
  border-radius: 4px;
  box-shadow: 1px 1px 3px rgba(0, 0, 0, 0.2);
  
}
form {
    display: flex;
    align-items: center;
    justify-content: space-around;
    flex-wrap: wrap;
}
.card h2 {
    color: #2A6A54;
    text-align: start;
  
}
.card button {
    max-width: 100px;
    background:#00A98F;
    color: white;
    text-align: center;
    margin-bottom: 10px;
    padding: 0;
    cursor: pointer;
}

</style>