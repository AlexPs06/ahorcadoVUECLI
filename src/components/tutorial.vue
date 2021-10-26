<template>
   <v-dialog
       transition="dialog-bottom-transition"
        v-model="tutorial"
        max-width="100%"
        persistent
      >
     
        <v-carousel show-arrows-on-hover v-model="model" :cycle="false">

            <template v-slot:prev="{ on, attrs }">
                <v-btn
                    color="primary"
                    v-bind="attrs"
                    v-on="on"
                >Anterior</v-btn>
            </template>
            <template v-slot:next="{ on, attrs }">
                <v-btn
                    color="primary"
                    v-bind="attrs"
                    v-on="on"
                >Siguiente</v-btn>
            </template>
            <v-carousel-item
            
            >
                <v-sheet
                    :color="colors[0]"
                    height="100%"
                    tile
                >
                
                    <v-row
                    class="fill-height"
                    align="center"
                    justify="center"
                    >
                        <div class="text-h2 ">
                            <v-card class="text-center">
                                <v-toolbar
                                color=" black--text text-h5 grey lighten-2"
                                dark
                                >
                                Bienvenido al juego del ahorcado edición Bioinformatica
                                </v-toolbar>
                                <v-card-text class="black--text text-h6">
                                    A continuación te mostraremos explicaremos como se juega, recuerda que todo el material de referencia puedes encontrarlo <br>
                                    haciendo 
                                    <v-btn
                                    class="black--text"
                                    
                                        href="https://computacion.cs.cinvestav.mx/~aperez/Seminario1/Bioinformatica.pdf"
                                        target="_blank"
                                        text
                                    > 
                                        <span class="mr-2">click aqui</span> 
                                        <v-icon>mdi-open-in-new</v-icon>
                                    </v-btn>

                                </v-card-text>
                                <v-card-actions class="justify-end">
                                <v-btn
                                    text
                                    @click="closeDialog()"
                                >Close</v-btn>
                                </v-card-actions>
                            </v-card>
                          
                        </div>
                    </v-row>
                </v-sheet>
            </v-carousel-item>
            <v-carousel-item >
                <v-sheet
                    :color="colors[1]"
                    height="100%"
                    tile
                >
                    <v-row
                    class="fill-height"
                    align="center"
                    justify="center"
                    >
                        <div class="text-h2 ">
                            <v-card class="text-center">
                                <v-toolbar
                                color=" black--text text-h5 grey lighten-2"
                                dark
                                >
                                Primero 
                                </v-toolbar>
                                <v-card-text class="black--text text-h6">
                                    Selecciona la palabra que desees de la lista, recuerda que la respuesta a estas palabras estan ocultas.
                                    

                                    <!-- Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.  -->
                                </v-card-text>
                                <v-card-actions class="justify-end">
                                <v-btn
                                    text
                                    @click="closeDialog()"
                                >Close </v-btn>
                                </v-card-actions>
                            </v-card>
                        </div>
                    </v-row>
                </v-sheet>
            </v-carousel-item>
            <v-carousel-item >
                <v-sheet
                    :color="colors[2]"
                    height="100%"
                    tile
                >
                    <v-row
                    class="fill-height"
                    align="center"
                    justify="center"
                    >
                        <div class="text-h2 ">
                            <v-card class="text-center">
                                <v-toolbar
                                color=" black--text text-h5 grey lighten-2"
                                dark
                                >
                                Segundo 
                                </v-toolbar>
                                <v-card-text class="black--text text-h6">
                                    Utiliza la pista para deducir la palabra 
                                    

                                    <!-- Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.  -->
                                </v-card-text>
                                <v-card-actions class="justify-end">
                                <v-btn
                                    text
                                    @click="closeDialog()"
                                >Close </v-btn>
                                </v-card-actions>
                            </v-card>
                        </div>
                    </v-row>
                </v-sheet>
            </v-carousel-item>


            <v-carousel-item >
                <v-sheet
                    :color="colors[3]"
                    height="100%"
                    tile
                >
                    <v-row
                    class="fill-height"
                    align="center"
                    justify="center"
                    >
                        <div class="text-h2 ">
                            <v-card class="text-center">
                                <v-toolbar
                                color=" black--text text-h5 grey lighten-2"
                                dark
                                >
                                Tercero 
                                </v-toolbar>
                                <v-card-text class="black--text text-h6">
                                    Ingresa una de las letras que creas que contenga la palabra en el recuadro y dale click al boton de comprobar
                                    

                                    <!-- Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.  -->
                                </v-card-text>
                                <v-card-actions class="justify-end">
                                <v-btn
                                    text
                                    @click="closeDialog()"
                                >Close </v-btn>
                                </v-card-actions>
                            </v-card>
                        </div>
                    </v-row>
                </v-sheet>
            </v-carousel-item>

             <v-carousel-item >
                <v-sheet
                    :color="colors[4]"
                    height="100%"
                    tile
                >
                    <v-row
                    class="fill-height"
                    align="center"
                    justify="center"
                    >
                        <div class="text-h2 ">
                            <v-card class="text-center">
                                <v-toolbar
                                color=" black--text text-h5 grey lighten-2"
                                dark
                                >
                                Cuarto 
                                </v-toolbar>
                                <v-card-text class="black--text text-h6">
                                    Si tu letra esta en la palabra esta se iluminara en verde, en caso contrario avanzara el dibujo, recuerda no dejes que se complete <br>
                                    o perderas el juego.
                                    

                                    <!-- Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.  -->
                                </v-card-text>
                                <v-card-actions class="justify-end">
                                <v-btn
                                    text
                                    @click="closeDialog()"
                                >Close </v-btn>
                                </v-card-actions>
                            </v-card>
                        </div>
                    </v-row>
                </v-sheet>
            </v-carousel-item>

             <v-carousel-item >
                <v-sheet
                    :color="colors[5]"
                    height="100%"
                    tile
                >
                    <v-row
                    class="fill-height"
                    align="center"
                    justify="center"
                    >
                        <div class="text-h2 ">
                            <v-card class="text-center">
                                <v-toolbar
                                color=" black--text text-h5 grey lighten-2"
                                dark
                                >
                                Quinto 
                                </v-toolbar>
                                <v-card-text class="black--text text-h6">
                                    Cada vez que logres encontrar una palabra esta se revelara de la lista, buena suerte.
                                    

                                    <!-- Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.  -->
                                </v-card-text>
                                <v-card-actions class="justify-end">
                                <v-btn
                                    text
                                    @click="closeDialog()"
                                >Close </v-btn>
                                </v-card-actions>
                            </v-card>
                        </div>
                    </v-row>
                </v-sheet>
            </v-carousel-item>
        </v-carousel>
        
    </v-dialog>

</template>

<script lang="ts">
  import Vue from 'vue'
  export default Vue.extend({
    name: 'tutorial',

    data: () => ({
       model: 0,
      colors: [
        'primary',
        'secondary',
        'yellow darken-2',
        'red',
        'orange',
      ],
      tutorial:true,
    }),
    methods: {
        closeDialog(){
            this.$emit("selected",false)
            this.$data.tutorial=false;
        }
    },
    mounted: function () { 
    this.$root.$on('myEvent', (activated: boolean) => { // here you need to use the arrow function
        this.$data.tutorial=activated;
    })
    }
  })
</script>

