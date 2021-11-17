<template>
  <div class="card">
    <h2>RESERVAR</h2>
    <form ref="reservas" @submit.prevent>
      <input
        class="mx-input"
        style="max-width: 250px"
        type="text"
        placeholder="Nombre"
        v-model="content"
      />
      <date-picker
        
        placeholder="Fecha"
        type="date"
        v-model="startDate"
        format="YYYY-MM-DD"
      ></date-picker>
      <vue-timepicker
        close-on-complete
        placeholder="Hora de entrada"
        :minute-interval="15"
        v-model="startTime"
        format="HH:mm"
      ></vue-timepicker>
      <vue-timepicker
        close-on-complete
        placeholder="Hora de salida"
        :minute-interval="15"
        v-model="endTime"
        format="HH:mm"
      ></vue-timepicker>
      <button
        @click="validacionDate()"
        class="mx-input"
      >
        Guardar
      </button>
    </form>
    <div v-if="showError" class="error"><p>La fecha ingresada no es valida</p></div>
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
      showError: false,
    };
  },
  methods: {
    agregarReserva(reserva) 
        {this.$emit("agregarReserva", reserva);
        this.$refs.reservas.reset();},

    validacionDate(){
      let dateNow = new Date();
      let date = new Date(this.startDate);
      if(dateNow.getTime() > date.getTime()) {
        console.log("Fecha en pasado")
        this.showError = true;
            setTimeout(() => {
              this.showError = false;
            }, 3000)
      }
      else this.agregarReserva({
            content: this.content,
            date: this.startDate.toISOString().split('T')[0],
            start: this.startDate.toISOString().split('T')[0] + ' ' + this.startTime,
            end: this.startDate.toISOString().split('T')[0] + ' ' + this.endTime,
            startTime:this.startTime,
            endTime:this.endTime,
          }) 
        
      }
          
      },
      

      
    }
    
    
  

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
  color: #2a6a54;
  text-align: start;
}
.card button {
  max-width: 100px;
  background: #00a98f;
  color: white;
  text-align: center;
  margin-bottom: 10px;
  padding: 0;
  cursor: pointer;
}
.error {
  position: absolute;
  left: 50%;
  top:30%;
  transform: translateX(-50%);
  width: 30%;
  background: red;
}
</style>