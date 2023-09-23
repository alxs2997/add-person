<template>
  <div v-if="!personas.length" class="alert alert-info" role="alert">
    No se han agregado personas
  </div>
  <div id="tabla-personas" class="table-widget">
    <div class="separator">
      <span class="caption-container">
        <span class="table-title">
          <svg
            width="20"
            height="20"
            viewBox="0 0 20 20"
            fill="none"
            xmlns="http://www.w3.org/2000/svg"
          >
            <path
              fill-rule="evenodd"
              clip-rule="evenodd"
              d="M11.6775 1.3486C10.9695 2.1636 10.6875 7.2886 11.5105 8.1126C12.3335 8.9346 17.2785 8.5186 18.4665 7.5836C21.3245 5.3326 13.9375 -1.2534 11.6775 1.3486Z"
              stroke="#272727"
              stroke-width="1.5"
              stroke-linecap="round"
              stroke-linejoin="round"
            />
            <path
              fill-rule="evenodd"
              clip-rule="evenodd"
              d="M16.1372 11.79C17.2212 12.874 14.3472 19.054 8.65122 19.054C4.39722 19.054 0.949219 15.606 0.949219 11.353C0.949219 6.053 6.17822 2.663 7.67722 4.162C8.54022 5.025 7.56822 9.086 9.11622 10.635C10.6642 12.184 15.0532 10.706 16.1372 11.79Z"
              stroke="#272727"
              stroke-width="1.5"
              stroke-linecap="round"
              stroke-linejoin="round"
            />
          </svg>
          <span> Lista de personal</span>
        </span>
      </span>
    </div>
    <table class="table">
      <thead class="cabezera">
        <tr class="headers">
          <th class="sticky-left">Nombre</th>
          <th>Apellido</th>
          <th>Email</th>
          <th class="sticky-right">Acciones</th>
        </tr>
      </thead>
      <tbody>
        <tr class="content" v-for="persona in personas" :key="persona.id">
          <td v-if="editando === persona.id">
            <input type="text" class="form-control" v-model="persona.nombre" />
          </td>
          <td v-else>{{ persona.nombre }}</td>
          <td v-if="editando === persona.id">
            <input
              type="text"
              class="form-control"
              v-model="persona.apellido"
            />
          </td>
          <td v-else>{{ persona.apellido }}</td>
          <td v-if="editando === persona.id">
            <input type="email" class="form-control" v-model="persona.email" />
          </td>
          <td v-else>{{ persona.email }}</td>
          <td class="more" v-if="editando === persona.id">
            <button class="btn-save" @click="guardarPersona(persona)">
              <i class="bx bxs-save"></i>
            </button>
            <button class="btn-cancel" @click="cancelarEdicion(persona)">
              <i class="bx bx-x"></i>
            </button>
          </td>
          <!--Sección de botones para acciones-->
          <td class="buttons">
            <button
              class="btn-eliminar"
              title="Eliminar persona"
              @click="$emit('delete-persona', persona.id)"
            >
              <i class="bx bx-trash"></i>
            </button>
            <button
              class="btn-editar"
              title="Editar persona"
              @click="editarPersona(persona)"
            >
              <i class="bx bx-edit"></i>
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
  },
  data() {
    return {
      editando: null,
    };
  },
  methods: {
    editarPersona(persona) {
      this.personaEditada = Object.assign({}, persona);
      this.editando = persona.id;
    },
    guardarPersona(persona) {
      if (
        !persona.nombre.length ||
        !persona.apellido.length ||
        !persona.email.length
      ) {
        return;
      }
      this.$emit("actualizar-persona", persona.id, persona);
      this.editando = null;
    },
    cancelarEdicion(persona) {
      Object.assign(persona, this.personaEditada);
      this.editando = null;
    },
  },
};
</script>
  
<style scoped>
#tabla-personas {
  margin-top: 20px;
}

#tabla-personas table {
  width: 100%;
  border-collapse: collapse;
  border-spacing: 0;
}

#tabla-personas table thead {
  background-color: #f5f5f5;
}

#tabla-personas table thead tr th {
  padding: 10px;
  font-weight: bold;
  font-size: 1.2rem;
  color: #272727;
  border-bottom: 1px solid #e6e6e6;
}

.separator {
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
  gap: 5px;
}
.caption-container {
  font-size: 1.12rem;
  font-weight: 700;
  text-align: left;
  padding-top: 20px;
  padding-bottom: 16px;
  border-bottom: 2px solid var(--gray-background);
}

.caption-container {
  display: flex;
  width: 100%;
  align-items: center;
}

.caption-container {
    display: flex;
    align-items: center;
}

.caption-container svg {
    margin-top: -2px;
}


.table-widget {
  border-radius: 20px;
  padding: 24px;
  width: 768px;
  max-width: 100%;
  border: .5px solid rgb(190, 190, 190);
  box-shadow: 0px 4px 16px 0px rgba(148, 156, 169, 0.15);
  text-align: left;
}

.sticky-left {
    position: sticky;
    z-index: 1;
    top: 0;
    left: 0;
}

.sticky-right {
    position: sticky;
    z-index: 1;
    top: 0;
    right: 0;
}


.buttons {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 5px;
}

.headers {
  text-align: center;
  font-weight: bold;
  font-size: 1.2rem;
  color: #272727;
  padding: 10px;
  border-bottom: 1px solid #e6e6e6;
}

.content {
  text-align: center;
}

.btn-eliminar {
  background: none;
  border: #a0a7b1 solid 1px;
  color: #a0a7b1;
  transition: all 0.3s 
        ease-in-out;
  padding: 2px 8px;
  border-radius: 50%;
  cursor: pointer;
}

.btn-eliminar:hover {
  background: #ffffff;
  border: #ff0000 solid 1px;
  color: red;
}

.btn-editar {
  background: none;
  border: #a0a7b1 solid 1px;
  color: #a0a7b1;
  padding: 2px 8px;
  border-radius: 50%;
  cursor: pointer;
  transition: all 0.3s 
        ease-in-out;
}

.btn-editar:hover {
  background: #ffffff;
  border: blue solid 1px;
  color: blue;
}

.btn-save {
  background: rgb(185, 214, 185);
  color: #208806;
  border: none;
  padding: 2px 8px;
  border-radius: 50%;
  cursor: pointer;
}
.more {
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
  gap: 5px;
}

.btn-save:hover {
  background: #208806;
  color: #45ff17;
}

.btn-cancel {
  background: rgb(121, 121, 121);
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

#tabla-personas::-webkit-scrollbar {
    height: 12px;
}
  
#tabla-personas::-webkit-scrollbar-track {
    background: var(
        --gray-mid);
    border-radius: 6px;
}

#tabla-personas::-webkit-scrollbar-thumb {
    background: var(
        --gray);
    border-radius: 5px;
}

</style>