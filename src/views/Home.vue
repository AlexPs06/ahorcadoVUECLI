<template>
 <v-parallax
   height="100%"
    dark
     src="https://cdn.vuetifyjs.com/images/parallax/material2.jpg"
  >
  <hello-world />
   </v-parallax>
</template>

<script lang="ts">
  import Vue from 'vue'
  import HelloWorld from '../components/HelloWorld.vue'

  export default Vue.extend({
    name: 'Home',

    components: {
      HelloWorld,
    },
  })
</script>
