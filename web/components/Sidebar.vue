<template lang="pug">
.sidebar.d-flex
</template>

<script>
export default {}
</script>

<style lang="scss">
.sidebar {
  background: #fafbfc;
  height: 100vh;
  max-width: 125px;
  left: 0;

  @media screen and (max-width: 1200px) {
    display: none !important;
  }
}
</style>
