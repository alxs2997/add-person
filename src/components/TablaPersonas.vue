<template>
  <div v-if="!personas.length" class="alert alert-info" role="alert">
  No se han agregado personas
</div>
  <div id="tabla-personas">
    <table class="table">
      <thead>
        <tr class="acciones">
          <th>Nombre</th>
          <th>Apellido</th>
          <th>Email</th>
          <th>Acciones</th>
        </tr>
      </thead>
      <tbody>
        <tr class="content" v-for="persona in personas" :key="persona.id">
          <td>{{ persona.nombre }}</td>
          <td>{{ persona.apellido }}</td>
          <td>{{ persona.email }}</td>
          <td>
              <button class="btn-eliminar"
              title="Eliminar persona"
              @click="$emit('delete-persona', persona.id)"
              ><i class='bx bxs-eraser'></i></button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>
  
<script>
export default {
  name: "tabla-personas",
  props: {
    personas: Array,
  },
};
</script>
  
<style scoped>
#tabla-personas {
  margin-top: 20px;
}

#tabla-personas table {
  width: 100%;
}

#tabla-personas table thead {
  background-color: #f5f5f5;
}

.acciones {
  text-align: center;
}

.content {
  text-align: center;
}

.btn-eliminar {
  background: none;
  border: #f03f3f solid 1px;
  color: #f03f3f;
  padding: 5px 10px;
  border-radius: 50%;
  cursor: pointer;
}

.btn-eliminar:hover {
  background: #f03f3f83;
  color: #fff;
}

</style>