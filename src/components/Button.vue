<template>
  <button @click="onClick">
    <slot />
  </button>
</template>

<script>
export default {
  name: "Button",
  props: {
    onClick: {
      type: Function,
      required: true,
    },
  },
};
</script>

<style scoped>
button {
  background-color: var(--background-color-accent);
  color: #000;
  font-size: 1.5rem;
  padding: 1rem 2rem;
}
</style>
