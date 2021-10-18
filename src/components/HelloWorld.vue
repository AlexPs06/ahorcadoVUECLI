<template>
  <v-container>
    <v-row  class="ma-n3"  >
      
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

      <v-sheet class="text-center"  color="grey lighten-3" elevation="24" width="20%"    >
         
            <v-card 
              class="d-flex flex-wrap"
              max-width="100%"
              tile
            >
              <v-list rounded>
                <v-subheader>Palabras</v-subheader>
                <v-list-item-group
                  v-model="selectedItem"
                  color="primary"
                >
                  <v-list-item
                    v-for="(item, i) in words"
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
   <v-sheet class="text-center"  color="grey lighten-3" elevation="24" width="80%" height="1000"   style="max-height: 100%;  "  >
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
        <v-text-field
            
            class="palabra"
            placeholder="Introduce la letra"
            filled
            v-model="letra"
            
          >
            
          </v-text-field >
        </v-col>

          <v-col class="mb-4">
          <v-btn 
          v-on:click="checarLetra()"
          :disabled="intentosRestantes==0 || ganar==true "
          elevation="2" >
            Comprobar
          </v-btn>
        </v-col>

        <v-col class="mb-4">
          <v-btn 
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

          <v-card v-else-if="word[i] == ' ' "  color="gray">
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
          Ecosystem
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
</template>

<script lang="ts">
  import Vue from 'vue'
  import { mdiTwitter } from '@mdi/js';
  export default Vue.extend({
    name: 'HelloWorld',

    data: () => ({
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
