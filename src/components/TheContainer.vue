<template>
  <div class="container">
    <slot></slot>
  </div>
</template>

<script>
export default {

};
</script>

<style scoped>
.container {
  max-width: 540px;
  margin: 70px auto 52px auto;
}

@media screen and (max-width: 540px) {
  .container {
    margin: 40px 24px auto 24px;
  }
}

</style>
