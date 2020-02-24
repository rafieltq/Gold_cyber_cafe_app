<template>
    <div>
         <v-app-bar
      app
      color="orange"
      
    >
      <v-app-bar-nav-icon dark @click="drawer = !drawer"></v-app-bar-nav-icon>

      <v-toolbar-title @click="goto('/')">Gold Cyber Café</v-toolbar-title>

    </v-app-bar>

    
    
    <v-navigation-drawer absolute  dark temporary color="orange" v-model="drawer">

      <v-list-item link @click="goto('/')">
        <v-list-item-content >
          <v-list-item-title class="title">
            Gold Cyber Café
          </v-list-item-title>
          <v-list-item-subtitle>
            6to A informatica
          </v-list-item-subtitle>
        </v-list-item-content>
      </v-list-item>

      <v-divider></v-divider>

      <v-list v-for="(item,index) in items" :key="index"
        dense
        nav
        
      >
        <v-list-item link>

          <v-list-item-icon>
            <v-icon>{{item.icon}}</v-icon>
          </v-list-item-icon>

          <v-list-item-content @click="goto(item.route)">
            <v-list-item-title>{{item.text}}</v-list-item-title>
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
        drawer: false,
        items: [
        {text:'Ordenes',icon:'mdi-view-dashboard',route:'/ordenes'},
        {text:'Mesas',icon:'mdi-table',route:'/mesas'},
        {text:'Productos',icon:'mdi-cart',route:'/productos'},
      ]
      }
        
    },
    methods: {
    goto(route){
      this.$router.push(route);
    }
  }
}
</script>