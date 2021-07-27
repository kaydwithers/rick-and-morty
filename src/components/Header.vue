<template>
  <header>
    <h1>Header</h1>
    <input />
  </header>
</template>

<script>
export default {
  name: "HelloWorld",
  props: {
    msg: String,
  },
};
</script>

<style scoped>
header {
  padding: 4rem;
}
</style>
