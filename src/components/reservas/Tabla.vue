!<template>
  <div class="card">
    <table class="table">
      <tr>
        <th class="content">Nombre</th>
        <th class="date-time">Horario</th>
        <th class="accion">Accion</th>
      </tr>
      <tr v-for="(reserva, i) in items" :key="i" class="listaTabla">
        <td class="content oscuro">{{ reserva.content }}</td>
        <td class="date-time claro">{{"de " + reserva.startTime + " a " + reserva.endTime }}</td>
        
        <td class="accion"><button
        @click="
        $emit('eliminarReserva', reserva)
        "
         class="btn"><i class="fas fa-trash icon"></i></button></td>
      </tr>
    </table>
  </div>
</template>

<script>

export default {
  data() {
    return {
    }
  },
  props: {
    items: {
      type: Array,
      default: () => []
    }
  }
};
</script>

<style scoped>
.card {
  margin: 2rem 0;
  
}

.table {
  width: 100%;
}
.table tr {
color: #8C8C8C;
}


td {
  padding:1rem 0;
  border-bottom-style:ridge ;
 

}
.content {
  
  text-align: start;
}
.date-time {
 text-align: end;
}
.accion {
  text-align: center;
}
.oscuro {
  color: #474747;
  font-weight: 700;
}
.claro {
  color: #868686;
}

.btn {
  background: white;
  border-style: none;
  cursor: pointer;
}

.icon {
  font-size:18px;
  color: #CCCCCC;
}







</style>