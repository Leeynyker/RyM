<template>
  <transition>
    <div class="mascara-modal">
      <div class="envoltura-modal">
        <div class="tarjeta-modal">
          <h1 class="titulo-modal">Places Filter</h1>
          <va-form
            class="form-modal"
            tag="form"
            @submit.prevent="hacerBusqueda"
          >
            <va-input color="#227360" class="mt-3" label="Name" v-model="nameForm" />

            <va-input color="#227360" class="mt-3" label="Type" v-model="typeForm" />

            <va-input color="#227360" class="mt-3" label="Dimension" v-model="dimensionForm" />

            <va-button color="#227360" type="submit" class="mt-3"> Buscar </va-button>
          </va-form>
        </div>
        <div class="close-modal" @click="closeModal"></div>
      </div>
    </div>
  </transition>
</template>

<script>
export default {
  data() {
    return {
      nameForm: "",
      typeForm: "",
      dimensionForm: "",
    };
  },
  methods: {
    hacerBusqueda() {
      this.$emit("_hacerBusqueda", [
        this.nameForm,
        this.typeForm,
        this.dimensionForm,
      ]);
    },
    closeModal() {
      this.$emit("_closeModal", false);
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
  background-color: rgba(25, 25, 26, 0.548);
  transition: ocupacy 0.3 ease;
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
  width: 50%;
  padding: 15px;
  background-color: #d8d8d8;
  border-radius: 10px;
  position: absolute;
  overflow-x: hidden;
  overflow-y: auto;
}
.close-modal {
  width: 100vh;
}
.close-modal {
  width: 100vw;
  height: 100vh;
}
.titulo-modal {
  font-size: 1.5rem;
  color: rgb(46, 46, 46);
}
.form-modal {
  display: flex;
  flex-direction: column;
  width: 75%;
  margin: 20px auto;
}
</style>
