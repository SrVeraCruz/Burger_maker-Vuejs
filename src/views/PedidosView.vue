<template>
  <div class="pedidos">
    <Center>
      <h1>Gerenciar Pedidos:</h1>
      <Dashboard />
    </Center>
  </div>
</template>

<script>
import Dashboard from '../components/Dashboard.vue'
import Center from "../components/Center.vue"

export default {
  components: {
    Center,
    Dashboard
  }
}
</script>