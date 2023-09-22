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
          <td v-if="editando === persona.id">
              <input type="text" class="form-control" v-model="persona.nombre" />
          </td>
          <td v-else>{{ persona.nombre }}</td>
          <td v-if="editando === persona.id">
              <input type="text" class="form-control" v-model="persona.apellido" />
          </td>
          <td v-else>{{ persona.apellido }}</td>
          <td v-if="editando === persona.id">
              <input type="email" class="form-control" v-model="persona.email" />
          </td>
          <td v-else>{{ persona.email }}</td>
          <td class="more" v-if="editando === persona.id">
            <button class="btn-save" @click="guardarPersona(persona)"><i class='bx bxs-save'></i></button>
    <button class="btn-cancel" @click="cancelarEdicion(persona)"><i class='bx bx-x'></i></button>
          </td>
          <!--Sección de botones para acciones-->
          <td class="buttons">
              <button class="btn-eliminar"
              title="Eliminar persona"
              @click="$emit('delete-persona', persona.id)"
              ><i class='bx bxs-eraser'></i></button>
              <button class="btn-editar" title="Editar persona" 
              @click="editarPersona(persona)">
              <i class='bx bx-edit'></i>
            </button>
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
  },data() {
        return {
            editando: null,
        }
    },
    methods: {
        editarPersona(persona) {
            this.personaEditada = Object.assign({}, persona);
            this.editando = persona.id;
        },
        guardarPersona(persona) {
            if (!persona.nombre.length || !persona.apellido.length || !persona.email.length) {
                return;  
            }
            this.$emit('actualizar-persona', persona.id, persona);
            this.editando = null;
        },
        cancelarEdicion(persona) {
            Object.assign(persona, this.personaEditada);
            this.editando = null;
        }
    }
}
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

.buttons {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 5px
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
  padding: 2px 8px;
  border-radius: 50%;
  cursor: pointer;
}

.btn-eliminar:hover {
  background: #f03f3f62;
  color: red;
}

.btn-editar{
  background: none;
  border: #003b94 solid 1px;
  color: #003b94 ;
  padding: 2px 8px;
  border-radius: 50%;
  cursor: pointer;
}

.btn-editar:hover {
  background: #003b9463;
  color: blue;
}

.btn-save{
  background: rgb(185, 214, 185) ;
  color: #208806;
  border: none;
  padding: 2px 8px;
  border-radius: 50%;
  cursor: pointer;
}
.more{
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
  gap: 5px;
}

.btn-save:hover {
  background: #208806;
  color: #45ff17;;
}

.btn-cancel{
  background: rgb(121, 121, 121) ;
  color: #ffffff;
  border: none;
  padding: 2px 8px;
  border-radius: 50%;
  cursor: pointer;
}

.btn-cancel:hover {
  background: #444444;
  color: #ff0000;
}
</style>