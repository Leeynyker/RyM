<template>
  <transition>
    <div class="mascara-modal">
      <div class="envoltura-modal">
        <div class="tarjeta-modal">
          <h1 class="titulo-modal">Filtrar personajes</h1>
          <form class="modal-form" @submit.prevent="hacerBusqueda">
            <va-input color="#227360" label="Nombre" v-model="namer" />

            <va-select
              class="mt-3"
              label="Estatus"
              v-model="valueStatus"
              :options="optionsStatus"
              color="#227360"
              clearable
            />
            <va-input color="#227360" class="mt-3" label="Especie" v-model="specie" />
            <va-input color="#227360" class="mt-3" label="Tipo" v-model="type" />
            <va-select
              class="mt-3"
              label="Genero"
              v-model="valueGenero"
              :options="optionsGenero"
              clearable
              color="#227360"
            />
            <va-button color="#227360" type="submit" class="mt-3"> Buscar </va-button>
          </form>
        </div>
        <div class="close-modal" @click="cerrarModal"></div>
      </div>
    </div>
  </transition>
</template>

<script>
export default {
  data() {
    return {
      namer: "",
      valueStatus: "",
      specie: "",
      type: "",
      valueGenero: "",
      optionsStatus: ["alive", "dead ", "unknown"],
      optionsGenero: ["female", "male ", "genderless", "unknown"],
    };
  },
  methods: {
    cerrarModal() {
      this.$emit("_cerrarModal", false);
    },
    hacerBusqueda() {
      this.$emit("_realizarBusqueda", [this.namer, this.valueStatus, this.specie, this.type, this.valueGenero])
    },
  },
};
</script>

<style scoped>
.mascara-modal {
  position: fixed;
  z-index: 100;
  top: 0;
  left: 0;
  width: 100%;
  height: 100vh;
  background-color: #0808088c;
  transition: opacity 0.3 ease;
  overflow-y: auto;
  overflow-x: hidden;
}
.envoltura-modal {
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 150;
}
.tarjeta-modal {
  min-width: 50%;
  max-width: 90%;
  padding: 15px;
  background-color: #d8d8d8;
  border-radius: 5px;
  position: absolute;
  overflow-x: hidden;
  overflow-y: auto;
}
.close-modal {
  width: 100vw;
  height: 100vh;
}
.titulo-modal {
  font-size: 1.8rem;
  font-family: cursive;
  color: #212121;
}
.modal-form {
  display: flex;
  flex-direction: column;
  width: 75%;
  margin: 20px auto;
}
</style>