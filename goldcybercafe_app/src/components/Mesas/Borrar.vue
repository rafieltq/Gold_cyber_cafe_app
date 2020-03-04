<template>
  <div>
    <v-dialog v-model="show">
      <v-card>
        <v-card-title class="headline grey lighten-2" primary-title>Eliminar mesa</v-card-title>

        <v-card-text>
          <v-container>Desea eliminar este elemento?</v-container>
        </v-card-text>

        <v-divider></v-divider>

        <v-card-actions>
          <v-btn color="error" dark @click="$emit('confirm')">Eliminar</v-btn>
          <v-spacer></v-spacer>
          <v-btn color="orange" text @click="$emit('close')">Cancelar</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </div>
</template>

<script>
export default {
  props: ["show"]
};
</script>