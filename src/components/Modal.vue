<template>
  <div class="modal">
    <div class="modal__overlay" @click="handleClose" />

    <div class="modal__content">
      <div>
        <Button @click="handleClose">✖</Button>
      </div>

      <div v-if="isLoading">
        <Loading />
      </div>

      <div v-else-if="!isLoading && error">
        <p>Something went wrong. Please try again.</p>
      </div>

      <div v-else-if="!isLoading && !character">
        <p>No character found.</p>
      </div>

      <div v-else>
        <img :alt="character.name" :src="character.image" />
        <h2>{{ character.name }}</h2>
        <p><strong>Species:</strong> {{ character.species }}</p>
        <p><strong>Location:</strong> {{ character.location.name }}</p>
        <p><strong>Status:</strong> {{ character.status }}</p>

        <Button @click="handleDropdown">Episodes</Button>

        <p>Episodes: {{ character.episode.length }}</p>
      </div>
    </div>
  </div>
</template>

<script>
import { API_URL } from "../js/const";

import Button from "./Button.vue";
import Loading from "./Loading.vue";

export default {
  name: "Modal",
  props: ["characterId"],
  data() {
    return {
      character: null,
      error: null,
      isLoading: false,
    };
  },
  components: {
    Button,
    Loading,
  },
  emits: ["close-modal"],
  methods: {
    /**
     * Get the character API response.
     *
     * @param {String} characterId - The characterId of the character.
     * @return {Promise}
     */
    getCharacter(characterId) {
      this.isLoading = true;
      this.error = null;

      fetch(API_URL + characterId)
        .then((response) => {
          if (response.ok) {
            return response.json();
          }
        })
        .then((data) => {
          this.isLoading = false;
          this.character = data;
        })
        .catch((error) => {
          console.error(`Failed getCharacter(): ${error}`);
          this.isLoading = false;
          this.error = error;
        });
    },

    /**
     * Handle the click of the close button.
     */
    handleClose() {
      this.$emit("close-modal");
    },

    /**
     * Handle the click of the dropdown button.
     */
    handleDropdown() {},
  },
  mounted() {
    this.getCharacter(this.characterId);
  },
};
</script>

<style scoped>
.modal {
  position: fixed;
  display: flex;
  height: 100%;
  align-items: center;
  justify-content: center;
  left: 0;
  top: 0;
  width: 100%;
}

.modal__overlay {
  position: absolute;
  background-color: #1a202c;
  height: 100%;
  left: 0;
  opacity: 0.5;
  width: 100%;
}

.modal__content {
  background-color: #fff;
  display: flex;
  flex-direction: column;
  height: 50%;
  justify-content: center;
  margin: 4rem;
  padding: 4rem;
  text-align: center;
  width: 100%;
  z-index: 1;
}

.modal__content img {
  margin-bottom: 2rem;
}

h2 {
  margin-bottom: 1rem;
}

p {
  margin-bottom: 0.5rem;
}
</style>
