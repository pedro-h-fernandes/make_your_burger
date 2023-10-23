<template>
  <Banner />
  <main class="main-container">
    <div>
      <h1>Monte o seu burger:</h1>
      <BurgerForm />
    </div>
    <img src="public\img\undraw_hamburger_re_7sfy.svg" alt="">

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
h1 {
  text-align: left;
}

main {
  display: flex;
  flex-direction: row;
  justify-content: space-evenly;
  align-items: center;
}
</style>
