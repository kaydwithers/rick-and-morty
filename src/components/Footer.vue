<template>
  <footer>
    <h1>Footer</h1>
  </footer>
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
footer {
  background-color: rgb(158, 158, 158);
  padding: 4rem;
}
</style>
