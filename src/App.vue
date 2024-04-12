<template>
  <NavBar :logo="logo_src" :alt="app_name" />
  <router-view/>
  <Footer />
</template>

<script>
import NavBar from "./components/NavBar.vue"
import Footer from "./components/Footer.vue"
export default {
  components: {
    NavBar,
    Footer
  },
  data() {
    return {
      logo_src: "/img/logo.png",
      app_name: "Make your Burger"
    }
  }
}
</script>

<style lang="scss">
  * {
    font-family: Helvetica;
    padding: 0;
    margin: 0;
    box-sizing: border-box;
  }

  a {
    text-decoration: none;
  }

  h1 {
    text-align: center;
    font-size: 2.5rem;
    margin-bottom: 1.5rem;
    color: #222;
  }
</style>
