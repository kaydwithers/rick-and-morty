<template>
  <li class="character">
    <button @click="handleCharacterSelect()">
      <img :alt="character.name" :src="character.image" />
      <p>{{ character.name }}</p>
    </button>
  </li>
</template>

<script>
export default {
  name: "Character",
  props: {
    character: {
      type: Object,
      required: false,
    },
  },
  emits: {
    "character-select": (id) => {
      if (id) {
        return true;
      } else {
        console.warn("id is missing.");
        return false;
      }
    },
  },
  methods: {
    /**
     * Handle the click of a character selection.
     */
    handleCharacterSelect() {
      this.$emit("character-select", this.character.id);
    },
  },
};
</script>

<style scoped>
button {
  align-items: center;
  background-color: var(--background-color-primary);
  border-radius: var(--border-radius);
  box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1),
    0 4px 6px -2px rgba(0, 0, 0, 0.05);
  display: flex;
  flex-direction: column;
  height: 100%;
  overflow: hidden;
  transition-duration: 300ms;
  transition-property: transform;
  width: 100%;
}

button:hover {
  transform: scale(1.05);
}

img {
  aspect-ratio: 1 / 1;
  object-fit: cover;
  width: 100%;
}

p {
  padding-bottom: 1rem;
  padding-top: 1rem;
}
</style>
