<template>
  <div id="app">
    <menubar />
    <nuevoedificio v-on:anexar="agregarEdificio" />
    <edificio
      v-for="k in edificios"
      :nombre="k.nombre"
      :pais="k.pais"
      :ano="k.ano"
      :altura="k.altura"
      :descripcion="k.descripcion"
      :srcimagen="k.srcimagen"
      :altimagen="k.altimagen"
      :key="k"
    />
  </div>
</template>

<script>
import nuevoedificio from "./components/nuevoedificio";
import edificio from "./components/edificio";
import menubar from "./components/menubar";
import axios from "axios";

export default {
  name: "App",

  components: {
    nuevoedificio,
    edificio,
    menubar,
  },

  data: function () {
    return {
      edificios: [],
    };
  },

  methods: {
    agregarEdificio: function (edif) {
      this.edificios.push(edif);
    },
    consultarEdificios: function () {
      axios
        .get("http://localhost:8000/edificios")
        .then((respuesta) => {
          this.edificios = respuesta.data;
        })
        .catch((error) => {
          alert("No funcionó");
        });
    },
    crearEdificio: function (edificio) {
      axios
        .post("http://localhost:8000/nuevo", edificio)
        .then((respuesta) => {
          let confirmacion = respuesta.data.mensaje;
          alert(confirmacion);
        })
        .catch((error) => {
          alert("No funcionó el método");
        });
    },
  },
  created: function () {   
    this.consultarEdificios();
  },
};
</script>

<style>
* {
  margin: 0;
  box-sizing: border-box;
}

#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /*text-align: center;*/
  color: #2c3e50;
}
#div-listar {
  border: 1px solid #000000;
  cursor: pointer;
}
</style>
