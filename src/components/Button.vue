<template>
  <input type="submit" class="submit-btn" :value="value">
</template>

<script>
export default {
  name: "ButtonModel",
  props: {
    value: ""
  }
}
</script>

<style scoped lang="scss">
  .submit-btn {
    color: #fcba03;
    font-weight: bold;
    background-color: #222;
    border: .1rem solid #222;
    border-radius: .2rem;
    padding: 0.5rem;
    font-size: 1rem;
    transition: .2s ease-in-out;
    cursor: pointer;

    &:hover {
      background: transparent;
      color: #222;
    }
  }
</style>