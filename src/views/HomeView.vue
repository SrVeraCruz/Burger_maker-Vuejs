<template>
  <div class="home">
    <Banner />
    <Center>
      <h1>Monte o seu Burger:</h1>
      <BurgerForm />
    </Center>
  </div>
</template>

<script>
import Center from "../components/Center.vue"
import Banner from "../components/Banner.vue"
import BurgerForm from "../components/BurgerForm.vue"

export default {
  components: {
    Center,
    Banner,
    BurgerForm
  }
}
</script>