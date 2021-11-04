!<template>
  <div class="card">
    <table>
      <tr>
        <th>Nombre</th>
        <th>Horario</th>
        <th>Accion</th>
      </tr>
      <tr v-for="(reserva, i) in items" :key="i" class="listaTabla">
        <td class="content">{{ reserva.content }}</td>
        <td class="dateTime claro">{{"de " + reserva.startTime + " a " + reserva.endTime }}</td>
        
        <td class="dateTime oscuro"><button><i class="far fa-trash-alt"></i></button></td>
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
td {
  padding-top: 1rem;
  border-bottom-style:ridge ;


}
.content {
  width: 60%;
  text-align: start;
}
.dateTime {
  width: 20%;
  text-align: end;
}
.oscuro {
  color: #474747;
  
}
.claro {
  color: #868686;
}

button {
  background: white;
  border-style: none;
}

tr {
  text-align: start;
}



</style>