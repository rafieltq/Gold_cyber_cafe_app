<template>
  <v-container>
    <v-content>
      <v-layout>
        <v-flex>
          <v-btn color="info" @click="showCreateProductsDialog = true">Crear producto</v-btn>
          <v-data-table
            :loading="loading"
            :headers="headers"
            :items="productos"
            class="elevation-1"
          >
            <template v-slot:item.action="{ item }">
              <v-icon small class="mr-2" @click="editItem(item)">mdi-pencil</v-icon>
              <v-icon small @click="deleteItem(item)">mdi-delete</v-icon>
            </template>
          </v-data-table>
        </v-flex>
      </v-layout>
    </v-content>
    <create-products @close="closeDialog()" :show="showCreateProductsDialog"></create-products>
  </v-container>
</template>

<script>
import axios from "axios";
import createProducts from "@/components/Productos/Crear";
export default {
  mounted() {
    this.getProducts();
  },
  components: {
    createProducts
  },
  data() {
    return {
      productos: [],
      nombre: "",
      showCreateProductsDialog: false,
      precio: 0,
      loading: false,
      axiosOptions: {
        headers: { "Content-Type": "application/json" },
        rejectUnauthorized: false
      },
      headers: [
        { text: "Nombre", value: "nombre" },
        { text: "Precio", value: "precio" },
        { text: "Unidad de medida", value: "unidad_medida" },
        { text: "Acciones", value: "action", sortable: false }
      ]
    };
  },
  methods: {
    closeDialog() {
      (this.showCreateProductsDialog = false), this.getProducts();
    },
    getProducts() {
      axios
        .get(
          "http://localhost/gold_cyber_cafe_api/productos/productos",
          this.axiosOptions
        )
        .then(response => {
          this.productos = response.data;
        })
        .catch(error => {
          console.log(error);
        });
    },
    deleteItem(item) {
      let request = confirm(`Está seguro que desea elminiar ${item.nombre} ? `);

      if (request === false) {
        return;
      }

      this.loading = true;

      axios
        .delete(
          `http://localhost/gold_cyber_cafe_api/productos/productos/${item.id}`,
          this.axiosOptions
        )
        .then(response => {
          this.getProducts();
          this.loading = false;
        })
        .catch(error => {
          console.log(error);
        });
    }
  }
};
</script>