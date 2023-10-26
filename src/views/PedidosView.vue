<template>
  <div class="main-container mb-lg">
    <h1 class="p-2 mb-2">Gerenciar pedidos:</h1>
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
