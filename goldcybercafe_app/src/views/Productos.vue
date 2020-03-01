<template>
  <v-container>
    <v-content>
      <v-layout>
        <v-flex>
          <v-btn
            class="mb-2"
            color="orange"
            dark
            @click="showCreateProductsDialog = true"
          >Crear producto</v-btn>
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
    <create-products @close="closeDialog('createProducts')" :show="showCreateProductsDialog"></create-products>
    <edit-products :item="itemTemp" :show="showEditDialog" @close="closeDialog('editProducts')"></edit-products>
    <delete-products-dialog :show="showDeleteDialog" @confirm="confirmDelete()" @close="closeDialog('deleteProductsDialog')"></delete-products-dialog>
    <v-snackbar
      top
      right
      color="success"
      v-model="snackbar"
    >
      Acción realizada correctamente
      <v-btn text @click="snackbar = false"><v-icon>mdi-check</v-icon></v-btn>
    </v-snackbar>

  </v-container>
</template>

<script>
import axios from "axios";
import createProducts from "@/components/Productos/Crear";
import editProducts from "@/components/Productos/Editar";
import deleteProductsDialog from "@/components/Productos/Borrar";
export default {
  mounted() {
    this.getProducts();
  },
  components: {
    createProducts,
    editProducts,
    deleteProductsDialog,
  },
  data() {
    return {
      productos: [],
      showEditDialog: false,
      nombre: "",
      showCreateProductsDialog: false,
      showDeleteDialog: false,
      itemTemp: {},
      snackbar: false,
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
    closeDialog(target) {
      if (target === "createProducts") {
        this.showCreateProductsDialog = false;
        this.snackbar = true
      } else if (target === 'deleteProductsDialog'){
        this.showDeleteDialog = false;
      }
      else {
        this.showEditDialog = false;
        this.snackbar = true
      }
      this.getProducts();
      
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

      this.showDeleteDialog = true
      this.itemTemp = item;
      
    },
    editItem(item) {
      this.itemTemp = item;
      this.showEditDialog = true;
    },
    confirmDelete(){
      axios
        .delete(
          `http://localhost/gold_cyber_cafe_api/productos/productos/${this.itemTemp.id}`,
          this.axiosOptions
        )
        .then(response => {
          this.getProducts();
          this.loading = false;
          this.snackbar = true;
          this.showDeleteDialog = false;
        })
        .catch(error => {
          console.log(error);
        });
    }
  }
};
</script>