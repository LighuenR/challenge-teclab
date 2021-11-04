<template>
  <div>
    <form @submit.prevent>
      <input class="mx-input" style="max-width: 250px" type="text" placeholder="Nombre" v-model="content" />
      <date-picker placeholder="Fecha"  type="date" v-model="startDate" format="YYYY-MM-DD"></date-picker>
      <vue-timepicker placeholder="Hora de entrada" :minute-interval="15" v-model="startTime" format="hh:mm"></vue-timepicker>
      <vue-timepicker placeholder="Hora de salida" :minute-interval="15" v-model="endTime" format="hh:mm"></vue-timepicker>
      <button
        @click="
          $emit('agregarReserva', {
            content: content,
            start: startDate.toISOString().split('T')[0] + ' ' + startTime,
            end: startDate.toISOString().split('T')[0] + ' ' + endTime,
          })
        "
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
};
</script>

<style lang="scss" scoped>
</style>