<template>
  <div class="center">
    <slot></slot>
  </div>
</template>

<script>
export default {
  name: "Center"
}
</script>

<style scoped lang="scss">
  .center {
    margin: 3rem;
    min-height: 20rem;
  }
</style>