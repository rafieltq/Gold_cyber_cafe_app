<template>
    <v-container>
        <v-content>
            <v-layout wrap>
                <v-flex v-for="(mesa,index) in mesas" :key="index">
                    <v-card
                    width="95"
                    height="95"
                    color="green"
                    class="mt-2 ml-2"
                    dark
                    >
                        <v-card-title>{{mesa.titulo}} {{mesa.numero}}</v-card-title>
                    </v-card>
                </v-flex>
            </v-layout>

            
        </v-content>
    </v-container>
</template>

<script>
export default {
    name: 'Mesas',
    data() {
        return {
            mesas: [
                {titulo:'Mesa',numero:'01'},
                {titulo:'Mesa',numero:'02'},
                {titulo:'Mesa',numero:'03'},
                {titulo:'Mesa',numero:'04'},
                {titulo:'Mesa',numero:'05'},
                {titulo:'Mesa',numero:'06'},
                {titulo:'Mesa',numero:'07'},
                {titulo:'Mesa',numero:'08'},
                {titulo:'Mesa',numero:'09'},
                {titulo:'Mesa',numero:'10'},
                {titulo:'Mesa',numero:'11'},
                {titulo:'Mesa',numero:'12'},
                {titulo:'Mesa',numero:'13'},
                {titulo:'Mesa',numero:'14'},
                {titulo:'Mesa',numero:'15'},
                {titulo:'Mesa',numero:'16'},
                {titulo:'Mesa',numero:'17'},
            ]
        }
    },
}
</script>