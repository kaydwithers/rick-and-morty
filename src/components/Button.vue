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
  background-color: papayawhip;
  cursor: pointer;
  font-size: 1.5rem;
  padding: 1rem 2rem;
}
</style>
