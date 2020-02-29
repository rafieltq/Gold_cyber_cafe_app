<template>
  <div>
    <v-dialog v-model="show" width="500">
      <v-card :loading="loading">
        <v-card-title class="headline grey lighten-2" primary-title>Crear producto</v-card-title>

        <v-card-text>
          <v-form v-model="valid">
            <v-container>
              <v-row>
                <v-col cols="12" md="4">
                  <v-text-field
                    v-model="product.nombre"
                    :rules="requireInputRule"
                    label="Nombre"
                    required
                  ></v-text-field>
                </v-col>

                <v-col cols="12" md="4">
                  <v-text-field
                    type="number"
                    v-model="product.precio"
                    :rules="requireInputRule"
                    label="precio"
                    required
                  ></v-text-field>
                </v-col>

                <v-col cols="12" md="4">
                  <v-text-field
                    v-model="product.unidad_medida"
                    :rules="requireInputRule"
                    label="Unidad de medida"
                    required
                  ></v-text-field>
                </v-col>
              </v-row>
            </v-container>
          </v-form>
        </v-card-text>

        <v-divider></v-divider>

        <v-card-actions>
          <v-btn color="success" @click="saveProduct()">Guardar</v-btn>
          <v-spacer></v-spacer>
          <v-btn color="error" @click="$emit('close')">Cerrar</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  props: ["show"],
  data: () => ({
    valid: false,
    requireInputRule: [v => !!v || "Este campo es requerido"],
    product: {
      nombre: "",
      precio: 0,
      unidad_medida: "unidad"
    },
    loading: false,

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
          "http://localhost/gold_cyber_cafe_api/productos/productos",
          this.product,
          options
        )
        .then(response => {
          this.$emit('close');
          this.loading = false;
        })
        .catch(error => {
          console.log(error);
        });
    }
  }
};
</script>