<template>
  <div class="main-container container-center mb-lg">
    <h1 class="p-2 my-3">Gerenciar pedidos:</h1>
    <Dashboard/>
  </div>
</template>

<script>
import Dashboard from '../components/Dashboard.vue';

  export default {
    name: 'PedidosView',
    components: { Dashboard }
}
</script>

<style></style>
