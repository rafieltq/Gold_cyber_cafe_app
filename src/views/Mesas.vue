<template>
  <v-container>
    <v-content>
      <v-btn color="orange" class="mb-2" dark @click="showCreateMesaDialog = true">Crear mesa</v-btn>
      <v-layout>
        <v-flex>
          <v-data-table :headers="headers" :items="mesas" class="elevation-1">
            <template v-slot:item.action="{ item }">
              <v-icon small class="mr-2" @click="editItem(item)">mdi-pencil</v-icon>
              <v-icon small class="mr-2" @click="deleteItem(item)">mdi-delete</v-icon>
            </template>
          </v-data-table>
        </v-flex>
      </v-layout>
    </v-content>
    <crear-mesa-dialog @close="closeDialog('crearMesa')" :show="showCreateMesaDialog"></crear-mesa-dialog>
    <edit-mesa :item="itemTemp" @close="closeDialog('editarMesa')" :show="showEditMesaDialog"></edit-mesa>
    <borrar-mesa @confirm="confirmDelete()" :show="showBorrarDialog" @close="closeDialog('borrarMesa')"></borrar-mesa>
    <v-snackbar :timeout="tiemout" top right color="success" v-model="snackbar">
      Acción realizada correctamente
      <v-btn text @click="snackbar = false">
        <v-icon>mdi-check</v-icon>
      </v-btn>
    </v-snackbar>
  </v-container>
</template>

<script>
import crearMesaDialog from '@/components/Mesas/Crear';
import editMesa from "@/components/Mesas/Editar";
import borrarMesa from '@/components/Mesas/Borrar'
import axios from "axios";
export default {
  name: "Mesas",
  mounted(){
    this.getMesas();
  },
  components:{
      crearMesaDialog,
      editMesa,
      borrarMesa,
  },
  data() {
    return {
      mesas: [],
      itemTemp:{},
      tiemout: 2000,
      snackbar: false,
      showCreateMesaDialog:false,
      showBorrarDialog:false,
      showEditMesaDialog: false,
      axiosOptions: {
        headers: { "Content-Type": "application/json" },
        rejectUnauthorized: false
      },
      headers: [
        {
          text: "Id",
          value: "id",
          align: "start",
          sortable: false,
        },
        { text: "Cantidad de personas", value: "cantidad_personas" },
        { text: "Descripción", value: "desripcion" },
        { text: "Estado", value: "disponible" },
        { text: "Acciones", value: "action", sortable: false }
      ]
    };
  },
  methods: {
    getMesas() {
      axios
        .get(
          "http://localhost/gold_cyber_cafe_api/mesas/mesas",
          this.axiosOptions
        )
        .then(response => {
          this.mesas = response.data;
        })
        .catch(error => {
          console.log(error);
        });
    },
    deleteItem(item) {
      this.showBorrarDialog = true;
      this.itemTemp = item;
    },
    confirmDelete() {
      axios
        .delete(
          `http://localhost/gold_cyber_cafe_api/mesas/mesas/${this.itemTemp.id}`,
          this.axiosOptions
        )
        .then(response => {
          this.getMesas();
          this.showBorrarDialog = false;
          this.snackbar = true;
        })
        .catch(error => {
          console.log(error);
        });
    },
    editItem(item) {
      this.itemTemp = item;
      this.showEditMesaDialog = true;
    },
    closeDialog(target) {
      if (target === "crearMesa") {
        this.showCreateMesaDialog = false;
        
      }else if (target === "editarMesa"){
        this.showEditMesaDialog = false;
      }else if (target === "borrarMesa"){
        this.showBorrarDialog = false;
      }
      this.snackbar = true;
      this.getMesas();
      
    },
  }
};
</script>