<template>
  <v-app>
    <v-app-bar
      app
      color="#1f272d"
      dark
    >
    <v-btn
        v-on:click="mostrarTutorial()"
        target="_blank"
        text
      >
        <span class="mr-2">Tutorial</span>
        <v-icon>mdi-open-in-new</v-icon>
      </v-btn>
      <!-- <div class="d-flex align-center">
        <v-img
          alt="Vuetify Logo"
          class="shrink mr-2"
          contain
          src="https://cdn.vuetifyjs.com/images/logos/vuetify-logo-dark.png"
          transition="scale-transition"
          width="40"
        />

        <v-img
          alt="Vuetify Name"
          class="shrink mt-1 hidden-sm-and-down"
          contain
          min-width="100"
          src="https://cdn.vuetifyjs.com/images/logos/vuetify-name-dark.png"
          width="100"
        />
      </div> -->

      <v-spacer></v-spacer>

      <v-btn
        href="https://computacion.cs.cinvestav.mx/~aperez/Seminario1/Bioinformatica.pdf"
        target="_blank"
        text
      >
        <span class="mr-2">Material de referencia</span>
        <v-icon>mdi-open-in-new</v-icon>
      </v-btn>
    </v-app-bar>

    <v-main>
      <tutorial   />
      <router-view/>
    </v-main>
  </v-app>
</template>

<script lang="ts">
import Vue from 'vue';
import tutorial from '../src/components/tutorial.vue';
export default Vue.extend({
  components: { tutorial },
  name: 'App',

  data: () => ({
    tuto:false,

    
  }),
   methods: {
      mostrarTutorial(){
        this.$root.$emit('myEvent', true);
        // $data.tutorial=true;
        // this.$refs.tutorial.;
      },
      closeDialog(data : boolean){
        this.$data.tuto=data
      }
    },
    
  
});
</script>
