<template>
  

<Navbar :logo="logo_src" :alt="app_name" />


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
  },

  data(){
    return{
      logo_src: "/img/carro.png",
      app_name: "Cadastre o carro no Estacionamento"
    }
  }

}

</script>

<style >

*{
  margin: 0px;
  padding: red;
  box-sizing: border-box;
  font-family: arial,arial,helvetica, sans-serif;
}

.main-container {
  margin: 40px;
  min-height: 250px;
  }

  h1 {
    text-align: center;
    font-size: 42px;
    margin-bottom: 40px;
    color: #222;

  }



</style>
