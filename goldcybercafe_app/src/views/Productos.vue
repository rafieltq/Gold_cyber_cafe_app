<template>
   <v-container>
       <v-content>
           <v-layout>
               <v-flex>
                   <v-card class="ma-4 green--text" v-for="(producto,index) in productos" :key="index">
                       <v-card-text>{{producto.nombre}}</v-card-text>
                       <v-chip class="ma-4" color="orange">$ {{producto.precio}}</v-chip>
                       <v-img width="100" height="100" ma-4 alt="La imagen" :src="productos.img"></v-img>
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
      .get("../database/productoh.json")
      .then(response => {
        this.productos = response.data;
      })
      .catch(error => {
        console.log(error);
      });
    },
    data(){
      
      return{
          productos:[]
      }
    }
            
    
    
}
</script>