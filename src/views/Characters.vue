<template>
  <div class="main-personajes">
    <div class="head-title">
      <h1 class="titulo">Personajes</h1>

      <va-button
        outline
        :rounded="false"
        flat
        class="mr-4 mb-2"
        color="#227360"
        @click="abrirModal"
      >
        <va-icon class="mr-1" name="filter_alt" color="dark" />
      </va-button>
    </div>
    <!-- <va-pagination v-model="value" :pages="0" /> -->
    <div class="paginator-content">
      <va-pagination
        class="paginator"
        color="#227360"
        v-model="page"
        boundary-numbers
        :pages="info.pages"
        :visible-pages="5"
        @click="getData()"
      />
    </div>

    <div class="contenedor">
      <va-card
        class="tarjeta"
        v-for="(personaje, index) in personajes"
        :key="index"
        :bordered="false"
        @click="abrirModalPersonaje(personaje)"
      >
        <va-image :src="personaje.image" style="height: 300px; border" />
        <va-card-title class="title-card">{{ personaje.name }}</va-card-title>
        <va-card-content
          >{{ personaje.species }} -
          <va-badge dot :color="status[`${personaje.status}`]">
            {{ personaje.status }}
          </va-badge>
        </va-card-content>
      </va-card>
    </div>

    <div class="paginator-content">
      <va-pagination
        class="paginator"
        color="#227360"
        v-model="page"
        boundary-numbers
        :pages="info.pages"
        :visible-pages="10"
        @click="getData()"
      />
    </div>
    <modal-personajes
      @_realizarBusqueda="buscar"
      @_cerrarModal="cerrarModal"
      v-if="verModal"
    />

    <va-modal v-model="verModalPersonaje" size="small">
      <template #content="{ ok }">
        <va-image :src="dataModalPersonaje.image" />
        <va-card-title class="title-card">{{
          dataModalPersonaje.name
        }}</va-card-title>
        <va-card-content>
          <div class="info">
            <p><b>Status: </b>{{ dataModalPersonaje.status }}</p>
            <p><b>Specie: </b>{{ dataModalPersonaje.species }}</p>
            <p><b>Type: </b>{{ dataModalPersonaje.type }}</p>
            <p><b>Gender: </b>{{ dataModalPersonaje.gender }}</p>
          </div>
          <va-accordion class="modal-accordion" v-model="despliegues" inset>
            <va-collapse
              :header="`Episodes: ${dataModalPersonaje.episode.length}`"
            >
              <div class="lista">
                <div
                  class="item-episode"
                  v-for="(episodio, i) in episidiosPersonajes"
                  :key="i"
                >
                  <p class="item-tetx">
                    {{ episodio.name }} - {{ episodio.episode }}.
                  </p>
                </div>
              </div>
            </va-collapse>
          </va-accordion>
        </va-card-content>
        <va-card-actions>
          <va-button @click="ok" color="#227360">Cerrar</va-button>
        </va-card-actions>
      </template>
    </va-modal>
  </div>
</template>

<script>
import ModalPersonajes from "@/components/personajes/ModalPersonajes.vue";
export default {
  components: { ModalPersonajes },
  data() {
    return {
      encabezados: {
        title1: "Info",
        title2: "Episodes",
      },
      verModal: false,
      verModalPersonaje: false,
      personajes: [],
      episidiosPersonajes: [],
      dataModalPersonaje: {},
      page: 1,
      info: {},
      status: { Alive: "success", Dead: "danger", unknown: "warning" },
      filtros: {
        gender: "",
        type: "",
        species: "",
        status: "",
        name: "",
      },
    };
  },
  methods: {
    getEpisode(episodios) {
      this.episidiosPersonajes = [];
      for (const episodio of episodios) {
        this.axios({
          method: "get",
          url: `${episodio}`,
        }).then((response) => {
          console.log(response);
          this.episidiosPersonajes.push(response.data);
        });
      }
    },
    getData() {
      const parametros = new URLSearchParams();
      parametros.append("name", this.filtros.name);
      parametros.append("status", this.filtros.status);
      parametros.append("species", this.filtros.species);
      parametros.append("type", this.filtros.type);
      parametros.append("gender", this.filtros.gender);
      parametros.append("page", this.page);
      this.axios({
        method: "get",
        url: "https://rickandmortyapi.com/api/character",
        params: parametros,
      }).then((response) => {
        this.personajes = response.data.results;
        this.info = response.data.info;
      });
    },
    abrirModal() {
      this.verModal = true;
    },
    abrirModalPersonaje(personaje) {
      this.verModalPersonaje = true;
      this.getEpisode(personaje.episode);
      this.dataModalPersonaje = personaje;
    },
    cerrarModal(data) {
      this.verModal = data;
    },
    SiguientePagina(next_url) {
      this.axios({
        method: "get",
        url: `${next_url}`,
      }).then((response) => {
        this.personajes = response.data.results;
        this.info = response.data.info;
      });
    },
    buscar(data) {
      this.verModal = false;
      this.filtros.name = data[0];
      this.filtros.status = data[1];
      this.filtros.species = data[2];
      this.filtros.type = data[3];
      this.filtros.gender = data[4];
      this.getData();
    },
  },
  mounted() {
    this.getData();
  },
};
</script>

<style scoped>
.tarjeta {
  /* border: 1px solid gray; */
  overflow: hidden;
  margin: 20px;
  width: 20%;
  min-width: 250px;
}
.tarjeta:hover {
  box-shadow: 3px 3px 18px 4px rgba(0, 0, 0, 0.329);
}
.main-personajes {
  width: 95vw;
  margin: auto;
}
.contenedor {
  margin: 30px auto;
  width: 100%;
  display: flex;
  flex-wrap: wrap;
  justify-content: space-evenly;
}
.titulo {
  color: rgb(60, 60, 60);
  font-size: 1.8rem;
  margin: 15px;
  font-family: cursive;
}
.head-title {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.title-card {
  font-size: 1rem;
}
.paginator {
  margin: auto;
}
.paginator-content {
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 10px 0px 25px 0px;
  /* background-color: #227360; */
}
.info {
  margin: 0 0 20px 0;
}
.lista {
  padding: 15px;
}
ul {
  display: block;
}
.item-tetx {
  margin: 15px 0;
}
</style>