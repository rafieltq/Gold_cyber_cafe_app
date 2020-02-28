<template>
  <v-container>
    <v-content>
      <v-layout>
        <v-flex>
          <v-card class="ma-4 green--text" v-for="(producto,index) in productos" :key="index">
            <v-card-text>{{producto.nombre}}</v-card-text>
            <v-chip class="ma-4" dark color="orange">$ {{producto.precio}}</v-chip>
            <v-img width="100" height="100" ma-4 alt="La imagen" :src="productos.img"></v-img>
          </v-card>
        </v-flex>
      </v-layout>
    </v-content>
  </v-container>
</template>

<script>
import axios from "axios";
export default {
  mounted() {
    this.saveProducts();
  },
  data() {
    return {
      productos: [],
      nombre: "",
      precio: 0
    };
  },
  methods: {
    saveProducts() {
      const options = {
        headers: { "Content-type": "application/json" },
        rejectUnauthorized: false
      };

      const data = {
        nombre: "tomate",
        precio: 50,
        unidad_medida: "unidad"
      };

      axios
        .post(
          "http://gibucket.a2hosted.com/gold_cyber_cafe_api/productos/productos",
          data,
          options
        )
        .then(response => {
          console.log(response.data);
        })
        .catch(error => {
          console.log(error);
        });
    }
  }
};
</script>