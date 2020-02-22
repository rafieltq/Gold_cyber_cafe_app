<template>
    <v-container>
        <v-content>
            <v-layout wrap>
                <v-flex 
                v-for="(orden,index) of ordenes" 
                :key="index"
                xs12
                
                >
                    <v-card
                      class="mt-2"
                      color="orange"
                      text
                      dark
                    >
                      <v-card-title>{{orden.titulo}} - {{orden.numero_orden}}</v-card-title>

                      <v-spacer></v-spacer>

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
export default {
    name: 'Ordenes',
    data() {
      return {
        ordenes: [
            {titulo: 'Orden',numero_orden: '1'},
            {titulo: 'Orden',numero_orden: '2'},
            {titulo: 'Orden',numero_orden: '2'}
          ]
      }
    },
}
</script>