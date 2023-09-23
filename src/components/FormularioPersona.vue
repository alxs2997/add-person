<template>
  <div id="formulario-persona">
    <form @submit.prevent="enviarFormulario">
      <div class="container">
        <div class="row">
          <div class="col-md-4">
            <div class="form-group">
              <label>Nombre:</label>
              <input
                ref="nombre"
                v-model="persona.nombre"
                type="text"
                class="form-control"
                :class="{ 'is-invalid': procesando && nombreInvalido }"
                @focus="resetEstado"
                @keypress="resetEstado"
                placeholder="Juan"
              />
            </div>
          </div>
          <div class="col-md-4">
            <div class="form-group">
              <label>Apellido:</label>
              <input
                v-model="persona.apellido"
                type="text"
                class="form-control"
                :class="{ 'is-invalid': procesando && apellidoInvalido }"
                @focus="resetEstado"
                placeholder="Castañeda"
              />
            </div>
          </div>
          <div class="col-md-4">
            <div class="form-group">
              <label>Email:</label>
              <input
                v-model="persona.email"
                type="email"
                class="form-control"
                :class="{ 'is-invalid': procesando && emailInvalido }"
                @focus="resetEstado"
                placeholder="correo@email.com"
              />
            </div>
          </div>
        </div>
        <div class="row">
          <div class="col-md-4">
            <div class="form-group">
              <button class="btn-env" title="Añadir Persona"><i class='bx bx-plus'></i> Añadir</button>
            </div>
          </div>
        </div>
      </div>
      <div class="container">
    <div class="row">
      <div class="col-md-12">
        <div v-if="error && procesando" class="alert alert-danger" role="alert">
          Debes rellenar todos los campos!
        </div>
        <div v-if="correcto" class="alert alert-success" role="alert">
          La persona ha sido agregada correctamente!
        </div>
      </div>
    </div>
  </div>
    </form>
  </div>
</template>
  
  <script>
export default {
  name: "formulario-persona",
  data() {
    return {
      procesando: false,
      correcto: false,
      error: false,
      persona: {
        nombre: "",
        apellido: "",
        email: "",
      },
    };
  },
  methods: {
    enviarFormulario() {
      this.procesando = true;
      this.resetEstado();

      // Comprobamos la presencia de errores
      if (this.nombreInvalido || this.apellidoInvalido || this.emailInvalido) {
        this.error = true;
        return;
      }

      this.$emit("add-persona", this.persona);
      this.$refs.nombre.focus();

      this.error = false;
      this.correcto = true;
      this.procesando = false;

      // Restablecemos el valor de la variables
      this.persona = {
        nombre: "",
        apellido: "",
        email: "",
      };
    },
    resetEstado() {
      this.correcto = false;
      this.error = false;
    },
  },
  computed: {
    nombreInvalido() {
      return this.persona.nombre.length < 1;
    },
    apellidoInvalido() {
      return this.persona.apellido.length < 1;
    },
    emailInvalido() {
      return this.persona.email.length < 1;
    },
  },
};
</script>
  
  <style scoped>
form {
  border-radius: 20px;
    padding: 24px;
    width: 768px;
    max-width: 100%;
    border: .5px solid rgb(190, 190, 190);
    box-shadow: 0px 4px 16px 0px 
        rgba(148, 156, 169, 0.15);
    text-align: left;
}

.container {
  padding: 1rem;
}

input {
  border-radius: 20px;
}
.btn-env {
  color: #000000;
  background: #fff;
  border-radius: 20px;
  padding: 0.5rem 1rem;
  cursor: pointer;
  transition: all 0.3s ease-in-out;
}
.btn-env:hover {
  background-color: #272727;
  color: #fff;
  border-radius: 20px;
}
</style>