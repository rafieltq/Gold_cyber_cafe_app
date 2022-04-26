<template>
  <v-container>
    <v-content>
      <v-layout wrap>
        <v-flex xs12>
			
		</v-flex>
      </v-layout>
    </v-content>
  </v-container>
</template>


<script>
import axios from "axios";
export default {
  mounted() {
    axios
      .get("../database/ordenes.json")
      .then(response => {
        this.pedidos = response.data;
      })
      .catch(error => {
        console.log(error);
      });
  },
  data() {
    return {
      pedidos: []
    };
  }
};
</script>