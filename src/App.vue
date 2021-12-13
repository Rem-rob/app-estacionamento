<template>
  

<Navbar />


  <router-view/> <!-- As views são impressas atraves deste carinha -->

<Footer />


</template>

<script>

import Navbar from './components/Navbar.vue' ;
import Footer from './components/Footer.vue' ;

export default {
  components: {
    Navbar,
    Footer
  }

}

</script>

<style>

</style>
