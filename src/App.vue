<template>
  <Modal />

  <Header />

  <main>
    <div v-if="isLoading">
      <p>Loading...</p>
    </div>

    <div v-else-if="!isLoading && error">
      <p>{{ error }}</p>
    </div>

    <div v-else-if="!isLoading && (!characters || characters.length === 0)">
      <p>No characters found.</p>
    </div>

    <div v-else>
      <Characters :characters="characters" />
    </div>
  </main>

  <Footer />
</template>

<script>
import Characters from "./components/Characters/index.vue";
import Footer from "./components/Footer.vue";
import Header from "./components/Header.vue";
import Modal from "./components/Modal.vue";

export default {
  name: "App",
  components: {
    Characters,
    Footer,
    Header,
    Modal,
  },
  data() {
    return {
      characters: [],
      error: null,
      isLoading: false,
    };
  },
  methods: {
    /**
     * Get the API response.
     *
     * @return {Promise}
     */
    getCharacters() {
      this.isLoading = true;
      this.error = null;

      fetch("https://rickandmortyapi.com/api/character")
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
          console.error(error);
          this.isLoading = false;
          this.error = `Failed getCharacters: ${error}`;
        });
    },
  },
  mounted() {
    this.getCharacters();
  },
};
</script>

<style>
body {
  margin: 0;
  padding: 0;
}
</style>
