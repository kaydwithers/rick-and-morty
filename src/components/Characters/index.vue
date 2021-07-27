<template>
  <div class="characters">
    <ul>
      <Character
        v-for="character in characters"
        :key="character.id"
        :character="character"
      />
    </ul>
  </div>
</template>

<script>
import Character from "./Character.vue";

export default {
  name: "Characters",
  components: {
    Character,
  },
  props: ["characters"],
};
</script>

<style scoped>
.characters {
  background-color: rgb(36, 40, 47);
}

ul {
  display: flex;
  flex-wrap: wrap;
  list-style: none;
  margin: 0;
  padding: 0;
}
</style>
