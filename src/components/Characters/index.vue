<template>
  <section>
    <h1>{{ randomName() }} &amp; {{ randomName() }}</h1>

    <div class="characters">
      <ul>
        <Character
          v-for="character in characters"
          :key="character.id"
          :character="character"
          @character-select="$emit('character-select', $event)"
        />
      </ul>
    </div>
  </section>
</template>

<script>
import Character from "./Character.vue";

export default {
  name: "Characters",
  components: {
    Character,
  },
  props: {
    characters: {
      type: Object,
      required: false,
    },
  },
  methods: {
    /**
     * Returns a random character name.
     *
     * @return {String}
     */
    randomName() {
      const index = Math.floor(Math.random() * this.characters.length);
      return this.characters[index].name;
    },
  },
};
</script>

<style scoped>
.characters {
  background-color: var(--background-color-secondary);
  padding: 4rem 2rem;
}

h1 {
  margin-bottom: 4rem;
  padding-left: 2rem;
  padding-right: 2rem;
  text-align: center;
}

ul {
  display: grid;
  grid-gap: 2rem;
  gap: 2rem;
  grid-auto-flow: row;
  grid-template-columns: repeat(2, 1fr);
}

@media (min-width: 768px) {
  ul {
    grid-template-columns: repeat(3, 1fr);
  }
}

@media (min-width: 1024px) {
  ul {
    grid-template-columns: repeat(6, 1fr);
  }
}

@media (min-width: 1280px) {
  .characters {
    padding: 4rem;
  }

  ul {
    grid-template-columns: repeat(7, 1fr);
  }
}
</style>
