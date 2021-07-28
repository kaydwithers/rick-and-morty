<template>
  <Modal />

  <Header
    v-model="searchText"
    @update:modelValue="getCharacters(`?name=${searchText}`)"
  />

  <main>
    <div v-if="isLoading">
      <p>Loading...</p>
    </div>

    <div v-else-if="!isLoading && error">
      <p>Something went wrong. Please try again.</p>
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
          console.log("data.results: ", data.results);
        })
        .catch((error) => {
          console.error(`Failed getCharacters(): ${error}`);
          this.isLoading = false;
          this.error = error;
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
