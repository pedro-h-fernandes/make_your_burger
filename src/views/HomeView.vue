<template>
  <Banner />
  <main class="main-container">
    <div>
      <h1>Monte o seu burger:</h1>
      <BurgerForm />
    </div>

    <picture>
      <source media="(min-width: 320px) and (max-width: 850px)" srcset="public\img\comendo-burger320.svg">
      <source srcset="public\img\comendo-burger.svg" alt="">
      <img src="public\img\comendo-burger.svg" alt="">
    </picture>

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
  flex-wrap: wrap;
  justify-content: space-evenly;
  align-items: center;
}

@media screen and (min-width: 320px) and (max-width: 768px) {
  img{ 
    margin-top: 30px;
  }
}
</style>
