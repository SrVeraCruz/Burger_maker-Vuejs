<template>
  <div id="nav">
    <router-link to="/" >
      <img :src="logo" :alt="alt" id="logo">
    </router-link>
    <div>
      <router-link to="/">Home</router-link>
      <router-link to="/pedidos">Pedidos</router-link>
    </div>
  </div>
</template>

<script>
export default {
  name: "NavBar",
  props: ["logo", "alt"]
}
</script>

<style scoped lang="scss">
  #nav {
    background-color: #222;
    border-bottom: .1rem solid #111;
    padding: 1rem 3rem;
    display: flex;
    justify-content: space-between;
    align-items: center;

    #logo {
      width: 2.5rem;
      height: 2.5rem;
    }

    a {
      color: #fcba03;
      margin: 0 0.7rem;
      transition: .3s ease-in-out;

      &:hover {
        color: #fff;
      }
    }
  }
</style>