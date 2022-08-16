
<style>
.white{
  color: #000;
  background-color: #fbfeff;
}
.red{
  color: rgb(250, 250, 250);
  background-color: #ca0a0a;
}
.green{
  color: rgb(243, 240, 240);
  background-color: #047404;
}
.blue{
  color: rgb(243, 243, 243);
  background-color: #0a779b;
}
.dark{
  color: rgb(248, 248, 248);
  background-color: #000000;
}

</style>
<template>
    <div>
        <v-row>
        <v-col
          cols="9"
          sm="9"
          md="9"
        >
          <v-text-field
            label="Numero Inicial"
            outlined
            type="number"
            v-model="numeroItem"
            min="1"
          ></v-text-field>
        </v-col>
        <v-col
        cols="3"
          sm="3"
          md="3">
            <v-btn
            depressed
            color="primary"
            style="background:#ddd"
            
            @click="calcularModulo()"
            >
            Enviar
            </v-btn>
        </v-col>
        </v-row>
        <v-card
            class="mx-auto"
            max-width="300"
            tile
        >
            <v-list dense>
            <v-subheader>operación módulo 5</v-subheader>
            <v-list-item-group
                
                color="primary"
            >
                <v-list-item
                v-for="(item, i) in items"
                :key="i"
                :class="item.clase"
                >
                
                <v-list-item-content>
                    <v-list-item-title v-text="item.valor" :class="item.clase"></v-list-item-title>
                </v-list-item-content>
                </v-list-item>
            </v-list-item-group>
            </v-list>
        </v-card>
    </div>
</template>
<script>
  import axios from "axios";
  // import { mdiVuetify } from '@mdi/js';
  const API_URL = "http://localhost:3000/api/";
  export default {
    data: () => ({
      // return {
        numeroItem: 1,
        items: [
            { valor: 1, clase: 'white' },
            { valor: 2, clase: 'red' },
            { valor: 3, clase: 'green' },
            { valor: 4, clase: 'blue' },
            { valor: 5, clase: 'dark' },
        ],
        
      // }
    }),
    computed: {
      
    },
    
    methods: {
        async calcularModulo(){
            await axios
            .post(API_URL+'numeroItem', {numero:this.numeroItem})
            .then(res => {
                console.log({res});
                this.items = res.data.resultado
            })
            .catch(err => {
                console.log({err});
            });
        }
      
    },
  }
</script>