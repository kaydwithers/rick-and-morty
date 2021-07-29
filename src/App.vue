<template>
  <Modal
    v-if="isModalOpen"
    :character-id="characterId"
    @close-modal="isModalOpen = false"
  />

  <Header
    v-model="searchText"
    @update:modelValue="getCharacters(`?name=${searchText}`)"
  />

  <main>
    <Loading v-if="isLoading" />

    <div v-else-if="!isLoading && error">
      <p>Something went wrong. Please try again.</p>
    </div>

    <div v-else-if="!isLoading && (!characters || characters.length === 0)">
      <p>No characters found.</p>
    </div>

    <Characters
      v-else
      :characters="characters"
      @character-select="handleCharacterSelect"
    />
  </main>

  <Footer
    @next-page="handleNextPage"
    @previous-page="handlePreviousPage"
  />
</template>

<script>
import { API_URL } from "./js/const";

import Characters from "./components/Characters/index.vue";
import Footer from "./components/Footer.vue";
import Header from "./components/Header.vue";
import Loading from "./components/Loading.vue";
import Modal from "./components/Modal.vue";

export default {
  name: "App",
  components: {
    Characters,
    Footer,
    Header,
    Loading,
    Modal,
  },
  data() {
    return {
      characterId: null,
      characters: [],
      currentPage: 1,
      error: null,
      isLoading: false,
      isModalOpen: false,
      searchText: null,
    };
  },
  methods: {
    /**
     * Get the API response.
     *
     * @param {String} param - The API url param.
     * @return {Promise}
     */
    getCharacters(param = "") {
      this.isLoading = true;
      this.error = null;

      fetch(API_URL + param)
        .then((response) => {
          if (response.ok) {
            return response.json();
          }
        })
        .then((data) => {
          this.isLoading = false;
          this.characters = data.results;
        })
        .catch((error) => {
          console.error(`Failed getCharacters(): ${error}`);
          this.isLoading = false;
          this.error = error;
        });
    },

    /**
     * Handle the click of a character selection.
     *
     * @param {String} id - The ID of the character.
     */
    handleCharacterSelect(id) {
      this.characterId = id;
      this.isModalOpen = true;
    },

    /**
     * Handle the click of the next page button.
     */
    handleNextPage() {
      this.currentPage++;
      this.getCharacters(`?page=${this.currentPage}`);
    },

    /**
     * Handle the click of the previous page button.
     */
    handlePreviousPage() {
      if (this.currentPage >= 1) {
        this.currentPage--;
        this.getCharacters(`?page=${this.currentPage}`);
      }
    },
  },
  mounted() {
    this.getCharacters();
  },
};
</script>

<style>
@import "./css/main.css";

#app {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
}
</style>
