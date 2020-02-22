<template>
    <div>
         <v-app-bar
      app
      color="orange"
      
    >
      <v-app-bar-nav-icon dark @click="drawer = !drawer"></v-app-bar-nav-icon>

      <v-toolbar-title>Gold Cyber Café</v-toolbar-title>

    </v-app-bar>

    
    
    <v-navigation-drawer absolute  dark temporary color="orange" v-model="drawer">

      <v-list-item>
        <v-list-item-content>
          <v-list-item-title class="title">
            Gold Cyber Café
          </v-list-item-title>
          <v-list-item-subtitle>
            6to A informatica
          </v-list-item-subtitle>
        </v-list-item-content>
      </v-list-item>

      <v-divider></v-divider>

      <v-list
        dense
        nav
        
      >
        <v-list-item link>

          <v-list-item-icon>
            <v-icon>mdi-view-dashboard</v-icon>
          </v-list-item-icon>

          <v-list-item-content @click="goto('ordenes')">
            <v-list-item-title>Ordenes</v-list-item-title>
          </v-list-item-content>
        </v-list-item>

         <v-list-item link>

          <v-list-item-icon>
            <v-icon>mdi-table</v-icon>
          </v-list-item-icon>

          <v-list-item-content @click="goto('Mesas')">
            <v-list-item-title>Mesas</v-list-item-title>
          </v-list-item-content>
        </v-list-item>

         <v-list-item link>

          <v-list-item-icon>
            <v-icon>mdi-help-box</v-icon>
          </v-list-item-icon>

          <v-list-item-content @click="goto('About')">
            <v-list-item-title>Sobre nosotros</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
        
      </v-list>
    </v-navigation-drawer>

    </div>
      
</template>

<script>
export default {
    name: 'TheNav',
    data(){
      return{
        drawer: false
      }
        
    },
    methods: {
    goto(route){
      this.$router.push(route);
    }
  }
}
</script>