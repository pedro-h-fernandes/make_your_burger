<template>
  <Banner />
  <main class="main-container">
    <h1>Monte o seu burger:</h1>
    <BurgerForm/>
  </main>
</template>


<script >
import Banner from '../components/Banner.vue';
import BurgerForm from '../components/BurgerForm.vue';

export default {
  components: {
    Banner,
    BurgerForm
  }
}
</script>

<style scoped>
  h1{
    text-align: left;
  }
  main {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }
</style>
