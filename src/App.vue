grava<template>
  <Navbar :logo="logo" :alt="alt" />
  <RouterView />
  <Footer />
</template>
 
<script>
import Navbar from './components/Navbar.vue';
import Footer from './components/Footer.vue';
import { RouterView } from 'vue-router'


export default {
  components: {
    Navbar,
    Footer
  },

  data() {
    return {
      logo: '/img/logo.png',
      alt: 'Logo da pagina. Um hamburger',
    }
  }
}
</script>

<style>
* {
  font-size: 62.5%;
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}

.main-container {
  margin: 80px 50px 50px 50px;
  min-height: 250px;
}

h1 {
  font-size: 4rem;
  text-align: center;
  margin-bottom: 30px;
  color: #222;
}
</style>
