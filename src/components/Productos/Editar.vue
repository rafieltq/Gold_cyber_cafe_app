<template>
  <div>
    <v-dialog v-model="show" width="500">
      <v-card :loading="loading">
        <v-card-title class="headline grey lighten-2" primary-title>Editar producto - {{item.nombre}}</v-card-title>

        <v-card-text>
          <v-form v-model="valid">
            <v-container>
              <v-row>
                <v-col cols="12" md="4">
                  <v-text-field
                    v-model="item.nombre"
                    :rules="requireInputRule"
                    label="Nombre"
                    required
                  ></v-text-field>
                </v-col>

                <v-col cols="12" md="4">
                  <v-text-field
                    type="number"
                    v-model="item.precio"
                    :rules="requireInputRule"
                    label="precio"
                    required
                  ></v-text-field>
                </v-col>

                <v-col cols="12" md="4">
                  <v-text-field
                    v-model="item.unidad_medida"
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
          <v-btn color="orange" dark @click="editProduct()">Guardar</v-btn>
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
  data() {
    return {
      requireInputRule: [v => !!v || "Este campo es requerido"],
      loading: false,
      valid: false,
    };
  },
  props: ["item",'show'],
  methods: {
    editProduct() {
      axios
        .put(
          `http://localhost/gold_cyber_cafe_api/productos/productos/${this.item.id}`,
          this.item,
          this.axiosOptions
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