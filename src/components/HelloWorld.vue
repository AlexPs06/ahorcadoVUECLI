<template>
   <!-- <v-parallax
   height="100%"
    dark
     src="https://cdn.vuetifyjs.com/images/parallax/material2.jpg"
.color1 {color: #060606;}
.color2 {color: #1f272d;}
.color3 {color: #3e535e;}
.color4 {color: #608094;}
.color5 {color: #87b6ce;}
  > -->
  <v-container  fluid class="fill-height">
  
    <v-row  class="fill-height ma-n3"  >
      
       <v-dialog
       transition="dialog-bottom-transition"
        v-model="ganarDialog"
        max-width="500px"
        persistent
      >
       <v-card class="text-center">
            <v-toolbar
            
              color="green"
              dark
            >Felicidades has ganado</v-toolbar>
            <v-card-text>
            </v-card-text>
            <v-card-actions class="justify-end">
              <v-btn
                text
                @click="ganarDialog = false"
              >Close</v-btn>
            </v-card-actions>
          </v-card>
      </v-dialog>

      <v-dialog
       transition="dialog-bottom-transition"
        v-model="perderDialog"
        max-width="500px"
        persistent
      >
       <v-card class="text-center">
            <v-toolbar
            
              color="red"
              dark
            >Una derrota no significa el final</v-toolbar>
            <v-card-text>
            </v-card-text>
            <v-card-actions class="justify-end">
              <v-btn
                text
                @click="perderDialog = false"
              >Close</v-btn>
            </v-card-actions>
          </v-card>
      </v-dialog>


      <!-- Lista de palabras -->

      <v-sheet class="text-center"  color="#87b6ce" elevation="24" width="20%"    >
         
            <v-card color="#608094"
              class="d-flex flex-wrap"
              max-width="100%"
              tile
            >
              <v-list color="#608094" rounded>
                <v-subheader>Palabras</v-subheader>
                <v-list-item-group
                  v-model="selectedItem"
                  color="cyan lighten-2"

                >
                  <v-list-item
                    v-for="(item, i) in palabras"
                    :key="i"
                    v-on:click="seleccionarPalabra(i)"
                  >
                    <v-list-item-icon>
                      <v-icon v-on:click="seleccionarPalabra(i)" v-text="'mdi-flag'"></v-icon>
                    </v-list-item-icon>
                    <v-list-item-content v-on:click="seleccionarPalabra(i)">
                      <v-list-item-title  v-text="item"></v-list-item-title>
                    </v-list-item-content>
                  </v-list-item>
                </v-list-item-group>
              </v-list>
            </v-card>

    </v-sheet>


  <!-- Juego del ahorcado -->
   <v-sheet class="text-center"  color="#87b6ce" elevation="24" width="80%" height="100%"   style="max-height: 100%;  "  >
      <v-col cols="12">
          <!-- :src="require('../assets/'{{foto}}'.jpg')" -->
          <!-- Imagen de que se muere -->
        <v-img
        :src="require('../assets/'+foto)"
          class="my-3"
          contain
          height="200"
        />
      </v-col>

      <v-col class="mb-4">
        <v-row >
        <v-col class="mb-4"> 
           <!-- <v-card max-height="60" max-width="200" > -->
      
            <v-text-field
                color="teal lighten-1"
                class="palabra white--text"
                placeholder="Introduce la letra"
                solo
                v-model="letra"
              >
              </v-text-field >
           <!-- </v-card> -->
        </v-col>

          <v-col class="mb-4">
          <v-btn 
          class="white--text"

          color="blue darken-4"
          v-on:click="checarLetra()"
          :disabled="intentosRestantes==0 || ganar==true "
          elevation="2" >
            Comprobar
          </v-btn>
        </v-col>

        <v-col class="mb-4">
          <v-btn 
          class="white--text"

          color="red darken-4"
          v-on:click="reiniciar()"
          elevation="2" >
            Reiniciar
          </v-btn>
        </v-col>
        
        </v-row>
        <!-- palabras dinamicas -->
        <h1 class="display-2 font-weight-bold mb-3">
          {{definiciones[posicion]  }}
          <v-row>
          <v-col v-for="(eco, i) in words[posicion]"
            :key="i">
         
                

          <v-card v-if="word[i] == trueWord[i]" color="green">
          <v-card-title  > {{ trueWord[i]}} </v-card-title>

          </v-card>

          <v-card v-else-if=" intentosRestantes==0 "  color="red">
          <v-card-title  > {{ trueWord[i]}} </v-card-title>
          </v-card>

          <v-card height="65" v-else-if="word[i] == ' ' "  color="#608094">
          <v-card-title  >  </v-card-title>
          </v-card>

          

          </v-col>
          
          </v-row>  
        </h1>

        <!-- texto de abajo -->
        <p class="subheading font-weight-regular">
          Si te interesa este tema y seguir aprendiendo sobre otros,
          <br>te recomiendo seguirnos en nuestro <a
            :href="'https://twitter.com/UnPocoDeCienci'"
            class="subheading mx-3"
            target="_blank"
          >
          <v-icon >{{icons[0]}}  </v-icon>
             
             Twitter
          </a>

        </p>
      </v-col>

      <v-col
        class="mb-5"
        cols="12"
      >
        <h2 class="headline font-weight-bold mb-3">
          Letras usadas:
        </h2>

        <v-row justify="center">
          <h3
            
            
            class="subheading mx-3"
            target="_blank"
          >
            {{ letras }}
          </h3>
        </v-row>
      </v-col>

      <v-col
        class="mb-5"
        cols="12"
      >
        <h2 class="headline font-weight-bold mb-3">
          Enlace al material de referencia
        </h2>

        <v-row justify="center">
          <a
            :href="'https://computacion.cs.cinvestav.mx/~aperez/Seminario1/Bioinformatica.pdf'"
            class="subheading mx-3"
            target="_blank"
          >
             Presentación
             
          </a>
        </v-row>
      </v-col>

      <v-col
        class="mb-5"
        cols="12"
      >
        <h2 class="headline font-weight-bold mb-3">
          Bioinformatica
        </h2>

        <!-- <v-row justify="center">
          <a
            v-for="(eco, i) in ecosystem"
            :key="i"
            :href="eco.href"
            class="subheading mx-3"
            target="_blank"
          >
            {{ eco.text }}
          </a>
        </v-row> -->

      </v-col>
      </v-sheet>

    </v-row>
  </v-container>
    <!-- </v-parallax> -->

</template>

<script lang="ts">
  import Vue from 'vue'
  import { mdiTwitter } from '@mdi/js';
  export default Vue.extend({
    name: 'HelloWorld',

    data: () => ({
      palabras:["Palabra 1","Palabra 2"],
      words:["bioinformatica","genoma"],
      definiciones:["Sinónimo biología computacional, informática biológica.","Es el conjunto de instrucciones genéticas que se encuentra en una célula"],
      posicion:0,
      icons:[mdiTwitter],
      word:[" "," "," "," "," "," "," "," "," "," "," "," "," "," "],
      trueWord:["b","i","o","i","n","f","o","r","m","a","t","i","c","a"],
      letra:"",
      letras:[],
      foto:'ahorcado5.jpg',
      intentosRestantes:5,
      selectedItem: 0,
      items: [
        { text: 'Real-Time', icon: 'mdi-clock' },
        { text: 'Audience', icon: 'mdi-account' },
        { text: 'Conversions', icon: 'mdi-flag' },
      ],
      ganar:false,
      ganarDialog:false,
      perder:false,
      perderDialog:false,
    }),
    methods: {
      checarLetra(){
        let letra = this.$data.letra; 
        let palabra = this.$data.words[this.$data.posicion];
        let correcto= false;
        for (let index = 0; index < palabra.length; index++) {
          if(palabra[index] == letra){
            this.$data.word[index] = letra;
            correcto=true;
          }
        }

        if( !this.$data.letras.includes(letra) ){
          this.$data.letras.push(letra)
        }

        
        if(!correcto){
          this.$data.intentosRestantes=this.$data.intentosRestantes-1
          this.$data.foto='ahorcado'+this.$data.intentosRestantes+'.jpg'
        }
        
        if(this.$data.intentosRestantes>0){
          this.$data.foto='ahorcado'+(this.$data.intentosRestantes-1)+'.jpg'
          this.$data.foto='ahorcado'+this.$data.intentosRestantes+'.jpg'
        }else{
           this.$data.perder=true;
           this.$data.perderDialog=true;

        }
        if(JSON.stringify(this.$data.word) === JSON.stringify(this.$data.trueWord) ){
          this.$data.ganar=true;
          this.$data.ganarDialog=true;
        }
        this.$data.letra="";

      },
      seleccionarPalabra( i : any){
        let palabra = this.$data.words[i];
        this.$data.posicion=i;
        let temp=[]; 
        let trueWord=[]; 
          for (let index = 0; index < palabra.length; index++) {
            temp.push(" ")
            trueWord.push(palabra[index]);
        }
        this.$data.trueWord=trueWord;
        this.$data.word=temp;

        this.$data.intentosRestantes=5;
        this.$data.foto='ahorcado'+this.$data.intentosRestantes+'.jpg'
        this.$data.letras=[]
        this.$data.ganar=false;
        this.$data.perder=false;
        this.$data.ganarDialog=false;
        this.$data.perderDialog=false;

      },
       reiniciar(){
         let palabra = this.$data.words[ this.$data.posicion];
        let temp=[]; 
        let trueWord=[]; 
          for (let index = 0; index < palabra.length; index++) {
            temp.push(" ")
            trueWord.push(palabra[index]);
        }
        this.$data.trueWord=trueWord;
        this.$data.word=temp;
        this.$data.intentosRestantes=5;
        this.$data.foto='ahorcado'+this.$data.intentosRestantes+'.jpg'
        this.$data.letras=[]
        this.$data.ganar=false;
        this.$data.perder=false;
        this.$data.ganarDialog=false;
        this.$data.perderDialog=false;

       }
    },
  })
</script>
<style scoped>
.letras{
      width: 100px;
}
.palabra{
      max-width: 200px;
}
</style>
