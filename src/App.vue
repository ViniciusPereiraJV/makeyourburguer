<template>
  <Navbar :logo="logo_src" :alt="app_name"/>
  <router-view/>
  <Footer/>
</template>

<script>
import Footer from './components/Footer.vue';
import Navbar from './components/Navbar.vue';

export default {
  name:"app",
  components:{Navbar, Footer},
  data(){
    return{
      logo_src:"/img/logo.png",
      app_name:"Maker Your Burguer"
    }
  }
}
</script>

<style>
*{
  font-family: Arial, Helvetica, sans-serif;
  padding:0;
  margin: 0;
  box-sizing: border-box;
}
.main-container{
  margin: 50px;
  min-height: 250px;
}
h1{
  text-align: center;
  font-size: 2em;
  margin-bottom: 30px;
  color: black;
}

</style>
