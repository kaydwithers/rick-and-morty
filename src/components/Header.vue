<template>
  <header>
    <label for="search">🔍</label>
    <input
      type="text"
      placeholder="Search"
      id="search"
      :value="modelValue"
      @input="$emit('update:modelValue', $event.target.value)"
    />
  </header>
</template>

<script>
export default {
  name: "Header",
  props: ["modelValue"],
  emits: ["update:modelValue"],
};
</script>

<style scoped>
header {
  align-items: center;
  display: flex;
  justify-content: center;
  padding: 4rem;
}

label {
  font-size: 2rem;
  margin-right: 1rem;
}

input {
  border-color: inherit;
  border-radius: 0.5rem;
  border-style: solid;
  border-width: 2px;
  font-size: 1rem;
  padding: 1rem;
}
</style>
