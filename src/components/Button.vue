<template>
  <button>
    <slot />
  </button>
</template>

<script>
export default { name: "Button" };
</script>

<style scoped>
button {
  background-color: papayawhip;
}
</style>
