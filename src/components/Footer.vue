<template>
  <footer>
    <button @click="$emit('previous-page')">⬅</button>
    <button @click="$emit('next-page')">➡</button>
  </footer>
</template>

<script>
export default {
  name: "Footer",
  emits: ["previous-page", "next-page"],
};
</script>

<style scoped>
footer {
  display: flex;
  justify-content: center;
  margin-top: auto;
  padding: 4rem 1rem;
}

button {
  font-size: 4rem;
  margin-left: 2rem;
  margin-right: 2rem;
}
</style>
