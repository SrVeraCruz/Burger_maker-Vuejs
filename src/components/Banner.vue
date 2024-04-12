<template>
  <div class="banner">
    <h1>Make your Burguer</h1>
  </div>
</template>

<script>

export default {
  name: "Banner"
}

</script>

<style scoped lang="scss">
  .banner {
    background-image: url('/public/img/burger.jpg');
    background-position: 0 -3rem;
    background-size: cover;
    background-repeat: no-repeat;
    height: calc(100vh);
    width: 100%;
    display: flex;
    align-items: center;
    justify-content: flex-start;
    
    h1 {
      color: #fff;
      background-color: #222;
      padding: 1.25rem 2.5rem;
      font-size: 3.5rem;
    }
    
    @media (max-width: 738px) {
      background-position: -20rem 0;
      align-items: center;
      justify-content: center;
      
      h1 {
        font-size: 1.8rem;
        padding: 1rem 2rem;
      }
    }

  }
</style>