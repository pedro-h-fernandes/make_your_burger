<template>
  <Navbar />
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
  }
}
</script>

<style></style>
