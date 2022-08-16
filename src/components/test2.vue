
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
.classbtn{
    margin: 4px !important;
    background-color: #000 !important;
    color: #ffff!important;
    padding: 8 !important;
    border-radius: 8 !important;
    text-transform: "uppercase" !important;
    padding-left: 32 !important;
    padding-right: 32 !important;
}
.numero{
    font-weight: bold;
    font-size: 70px;
}
</style>
<template>
    <div>
        <div class="text-center">
            <v-btn
            class="ma-2 classbtn"
            color="secondary"
            @click="operacion(1)"
            >
            add
            </v-btn>

            <v-btn
            class="ma-2 classbtn"
            color="secondary"
            @click="operacion(2)"
            >
            substract
            </v-btn>

            <v-btn
            class="ma-2 classbtn"
            color="secondary"
            @click="operacion(3)"
            >
            divide
            </v-btn>

            <v-btn
            class="classbtn"
            @click="operacion(0)"
            >
            reset
            </v-btn>

            
        </div>
        <div class="text-center numero">
            <div :class="clase" v-text="numeroItem"></div>
        </div>
        

        
    </div>
</template>
<script>
  import axios from "axios";
  // import { mdiVuetify } from '@mdi/js';
  const API_URL = "http://localhost:3000/api/";
  export default {
    data: () => ({
      // return {
        numeroItem: 0,
        clase:'',
      // }
    }),
    computed: {
      
    },
    
    methods: {
        async operacion(tipo){
            let operacion = 'suma';
            switch (tipo) {
                case 0: //resetea
                    // this.numeroItem = 0;
                    operacion = 'reset';
                    break;
                case 1: // suma 1 al original
                    // this.numeroItem += 1 ;
                    operacion = 'suma';
                    break;
                case 2: // resta 2 al contador
                    // this.numeroItem -= 2;
                    operacion = 'resta';
                    break;
                case 3: // divide por 3 al contador
                    // this.numeroItem = this.numeroItem / 3;
                    operacion = 'divide';
                    break;
                default:
                    break;
            }
            // residuo
            /*let numero = (this.numeroItem < 0) ? this.numeroItem * -1 : this.numeroItem;
            let res = parseInt(numero)  % 3;
            res = (res < 0) ? res * 1 : res
            switch (res) {
                case 0: this.clase='red'; break;
                case 1: this.clase='green'; break;
                case 2: this.clase='blue'; break;
                default:
                    break;
            }*/
            /// operacion back
            await axios
            .post(API_URL+operacion, {numero:this.numeroItem})
            .then(res => {
                console.log({res});
                this.numeroItem = res.data.numero;
                this.clase = res.data.clase
            })
            .catch(err => {
                console.log({err});
            });
        },
        
      
    },
  }
</script>