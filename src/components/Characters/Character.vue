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
  props: ["character"],
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
    handleCharacterSelect() {
      console.log("handleCharacterSelect");
      this.$emit("character-select", this.character.id);
    },
  },
};
</script>

<style scoped>
button {
  background-color: #fff;
  border-radius: 0.5rem;
  cursor: pointer;
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
  object-fit: cover;
  width: 100%;
}

p {
  padding-bottom: 1rem;
  padding-top: 1rem;
}
</style>
