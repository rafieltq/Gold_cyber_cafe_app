<template>
  <div>
    <v-dialog v-model="show" width="500">
      <v-card :loading="loading">
        <v-card-title class="headline grey lighten-2" primary-title>Crear mesa</v-card-title>
        <v-card-text>
          <v-form v-model="valid">
            <v-container>
              <v-row>
                <v-col cols="12" md="4">
                  <v-text-field
                    type="number"
                    v-model="table.cantidad_personas"
                    :rules="requireInputRule"
                    label="Cantidad de personas"
                    required
                  ></v-text-field>
                </v-col>

                <v-col cols="12" md="4">
                  <v-text-field
                    v-model="table.descripcion"
                    :rules="requireInputRule"
                    label="Descripción"
                    required
                  ></v-text-field>
                </v-col>

                <v-col cols="12" md="4">
                  <v-text-field
                    v-model="table.disponible"
                    :rules="requireInputRule"
                    label="Estado"
                    required
                  ></v-text-field>
                </v-col>

              </v-row>
            </v-container>
          </v-form>
        </v-card-text>

        <v-divider></v-divider>

        <v-card-actions>
          <v-btn color="orange" dark @click="saveProduct()">Guardar</v-btn>
          <v-spacer></v-spacer>
          <v-btn color="error" @click="$emit('close')">Cerrar</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </div>
</template>

<script>
import axios from "axios";
export default {
  props: ["show"],
  data: () => ({
    valid: false,
    requireInputRule: [v => !!v || "Este campo es requerido"],
    table: {
      id: "",
      cantidad_personas: 0,
      descripcion:"",
      disponible: 'si'
    },
    loading: false
  }),
  methods: {
    saveProduct() {
      this.loading = true;
      const options = {
        headers: { "Content-Type": "application/json" },
        rejectUnauthorized: false
      };
      axios
        .post(
          "http://localhost/gold_cyber_cafe_api/mesas/mesas",
          this.table,
          options
        )
        .then(response => {
          this.$emit("close");
          this.loading = false;
          this.table.cantidad_personas = 0;
          this.table.descripcion = "";
          this.table.disponible = "si";
         
        })
        .catch(error => {
          console.log(error);
        });
    }
  }
};
</script>