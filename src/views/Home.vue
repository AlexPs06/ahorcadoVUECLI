<template>

  
  <hello-world />
   
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
<style>
 .bg-image {
   background-repeat: no-repeat;
   background-position: center center;
   background-attachment: fixed;
   background-size: cover;
 }
</style>