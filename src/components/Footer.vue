<template>
  <footer>
    <button @click="$emit('previous-page')">⬅</button>
    <button @click="$emit('next-page')">➡</button>
  </footer>
</template>

<script>
export default {
  name: "Footer",
};
</script>

<style scoped>
footer {
  background-color: rgb(158, 158, 158);
  display: flex;
  justify-content: center;
  padding: 2rem;
}

button {
  cursor: pointer;
  font-size: 4rem;
  margin-left: 1rem;
  margin-right: 1rem;
}
</style>
