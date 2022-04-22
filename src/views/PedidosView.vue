<template>
  <div class="main-container">
    <h1>Gerenciar pedidos:</h1>
    <DashboardPedidos />
  </div>
</template>

<script>
import DashboardPedidos from "../components/Dashboard.vue"

export default {
  name: "PedidosBurger",
  components: {
    DashboardPedidos
  }
}
</script>
