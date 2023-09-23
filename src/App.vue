<template>
  <div id="app" class="container">
    <div class="row">
      <div class="col-md-12">
        <h1 class="title">Añadir Empleados</h1>
      </div>
    </div>
    <div class="row">
      <div class="col-md-12">
        <formulario-persona @add-persona="agregarPersona" />
        <tabla-personas
          :personas="personas"
          @delete-persona="eliminarPersona"
          @actualizar-persona="actualizarPersona"
        />
      </div>
    </div>
  </div>
</template>

<script>
import TablaPersonas from "@/components/TablaPersonas.vue";
import FormularioPersona from "@/components/FormularioPersona.vue";

export default {
  name: "app",
  components: {
    TablaPersonas,
    FormularioPersona,
  },
  data() {
    return {
      personas: [
        {
          id: 1,
          nombre: "Jon",
          apellido: "Nieve",
          email: "jon@email.com",
        },
        {
          id: 2,
          nombre: "Tyrion",
          apellido: "Lannister",
          email: "tyrion@email.com",
        },
        {
          id: 3,
          nombre: "Daenerys",
          apellido: "Targaryen",
          email: "daenerys@email.com",
        },
      ],
    };
  },
  methods: {
    agregarPersona(persona) {
      let id = 0;

      if (this.personas.length > 0) {
        id = this.personas[this.personas.length - 1].id + 1;
      }

      this.personas = [...this.personas, { ...persona, id }];
    },
    eliminarPersona(id) {
      this.personas = this.personas.filter((persona) => persona.id !== id);
    },
    actualizarPersona(id, personaActualizada) {
      this.personas = this.personas.map((persona) =>
        persona.id === id ? personaActualizada : persona
      );
    },
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Handjet:wght@300&family=Josefin+Sans:wght@200&family=Titillium+Web:wght@400;700&display=swap");

:root {
    --background: #ECECF4;
    --table-background: #FCFCFD;
    --primary: #272727;
    --gray: #A0A7B1;
    --odd-row: #f6f9ff;
    --th-background: #F4F5FC;
    --gray-background: #EDEEF1;
    --gray-mid: #F1F2F6;
}

* {
  font-family: "Handjet", cursive;
  font-family: "Josefin Sans", sans-serif;
  font-family: "Titillium Web", sans-serif;
}

body {
  margin: 0px;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    padding: 16px;
    background-color:var(--background);
}

button {
  background: var(--gray);
  border: 1px solid var(--primary);
}

.title {
  text-align: center;
  margin-bottom: 2rem;
  margin-top: 1.5rem;
  font-weight: bold;
}
</style>
