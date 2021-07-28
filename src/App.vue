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
    <div v-if="isLoading">
      <Loading />
    </div>

    <div v-else-if="!isLoading && error">
      <p>Something went wrong. Please try again.</p>
    </div>

    <div v-else-if="!isLoading && (!characters || characters.length === 0)">
      <p>No characters found.</p>
    </div>

    <div v-else>
      <Characters
        :characters="characters"
        @character-select="handleCharacterSelect"
      />
    </div>
  </main>

  <Footer
    :nextPage="nextPage"
    :previousPage="previousPage"
    @next-page="handleNextPage"
    @previous-page="handlePreviousPage"
  />
</template>

<script>
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
      nextPage: null,
      previousPage: null,
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
    getCharacters(param = null) {
      const url = `https://rickandmortyapi.com/api/character/${
        param ? param : ""
      }`;

      this.isLoading = true;
      this.error = null;

      fetch(url)
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
body {
  font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
  margin: 0;
  padding: 0;
}

h1,
h2,
h3,
p {
  margin: 0;
}

button {
  background-color: transparent;
  background-image: none;
  border-style: none;
  padding: 0;
}

ol,
ul {
  list-style: none;
  margin: 0;
  padding: 0;
}

h1 {
  font-size: 3rem;
  margin-bottom: 3rem;
}

p {
  font-size: 1rem;
}
</style>
