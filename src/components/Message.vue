<template>
  <div class="message-container">
    <p>{{ msg }}</p>
  </div>
</template>

<script>
export default {
  name: "Message",
  props: {
    msg: String
  }
}
</script>

<style scoped lang="scss">
  .message-container {
    color: 004085;
    background-color: #cce5ff;
    border: .1rem solid #b8daff;
    border-radius: .3rem;
    padding: 0.5rem;
    max-width: 18.5rem;
    margin: 1rem auto;
    text-align: center;
    font-weight: 600;
  }
</style>