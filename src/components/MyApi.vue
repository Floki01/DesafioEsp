<template>
  <button @click="mostrarPais" class="button m-5">Explorar paises</button>
  <div v-if="pais == null">Presiona el boton para comenzar</div>
  <div class="shadow border border-black" v-else>
    <h1>Nombre Comun: {{ this.pais.name.common}}</h1>
    <h1>Nombre oficial: {{ this.pais.name.official}}</h1>
    <h1>Region: {{ this.pais.region}}</h1>
    <h1>Capital: {{ this.pais.capital}}</h1>
    <h1>Poblacion: {{ this.pais.population}} habitantes</h1>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      data: [],
      pais: null,
    };
  },
  mounted() {
    this.fetchData();
  },
  methods: {
    fetchData() {
      axios
        .get("https://restcountries.com/v3.1/all")
        .then((response) => {
          this.data = response.data;
        })
        .catch((error) => {
          console.error(error);
        });
    },
    mostrarPais() {
      const i = Math.floor(Math.random() * this.data.length);
      this.pais = this.data[i];
    //   window.alert(JSON.stringify(this.pais));
    //   window.alert(Object.entries(this.pais));
    },
  },
};
</script>

