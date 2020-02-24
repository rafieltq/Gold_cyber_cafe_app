<template>
    <v-container>
        <v-content>
            <v-layout wrap>
                <v-flex xs12>
                    <v-card v-for="(pedido,index) in pedidos" 
                      :key="index"
                      class="mt-2"
                      color="orange"
                      text
                      dark
                    >
                    
                      <v-layout>
                        <v-card-text>{{pedido.id}}</v-card-text>
                        <v-card-text>{{pedido.fecha_creacion}}</v-card-text>
                        
                      </v-layout>

                      <v-spacer></v-spacer>
                      
                    
                      
                      <v-card-text v-for="(producto,index) in pedido.productos" :key="index">
                        {{producto.nombre}}
                      </v-card-text>


                      <v-card-actions>
                          <v-btn color="brown accent-4" text><v-icon left>mdi-pencil</v-icon> Orden Lista</v-btn>
                      </v-card-actions>

                    </v-card>
                </v-flex>
            </v-layout>
        </v-content>
    </v-container>
</template>


<script>
import axios from 'axios'
export default {
     mounted(){
    axios
      .get("../database/ordenes.json")
      .then(response => {
        this.pedidos = response.data
        
      })
      .catch(error => {
        console.log(error);
      });
    },
    data(){
      
      return{
          pedidos:[]
      }
    }
}
</script>