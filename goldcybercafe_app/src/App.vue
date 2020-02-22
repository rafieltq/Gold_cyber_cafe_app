<template>
  <v-app>
  
      <menucomponent></menucomponent>
  
    <v-content>
     <router-view></router-view>
    </v-content>
    
  </v-app>
</template>

<script>

import Menucomponent from '../src/components/TheNav.vue'

export default {
  name: 'App',

  components: {
    Menucomponent
  },
}
</script>
