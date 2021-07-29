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

    <button v-if="hasTheme" @click="handleTheme()">🌞</button>
    <button v-else @click="handleTheme('dark')">🌚</button>
  </header>
</template>

<script>
export default {
  name: "Header",
  props: {
    modelValue: {
      type: String,
      required: false,
    },
  },
  data() {
    return {
      hasTheme: false,
    };
  },
  emits: ["update:modelValue"],
  methods: {
    /**
     * Handle the click of the theme buttons.
     *
     * @param {String} theme - The theme to add.
     */
    handleTheme(theme = null) {
      this.hasTheme = !this.hasTheme;
      if (theme) {
        document.body.className = theme;
      } else {
        document.body.className = "";
      }
    },
  },
};
</script>

<style scoped>
header {
  align-items: center;
  display: flex;
  justify-content: center;
  padding: 4rem 1rem;
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
  width: auto;
}

button {
  font-size: 2rem;
  margin-left: 1rem;
}

@media (min-width: 768px) {
  input {
    width: 16rem;
  }
}
</style>
