!<template>
  <div class="tabla">
    <table>
      <tr>
        <th>Nombre</th>
        <th>Horario</th>
        <th>Accion</th>
      </tr>
      <tr v-for="(reserva, i) in items" :key="i" class="listaTabla">
        <td style="width: 60%" class="content">{{ reserva.content }}</td>
        <td>{{ reserva.start + " / " + reserva.end }}</td>
        <img src="../../assets/img/trash-alt-regular.svg" alt="">
        <td><button></button></td>
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
.tabla {
  padding: 1rem;
  margin: 1rem;
}

td {
  padding-top: 1rem;

}
.content {
  width: 50%;
}

</style>