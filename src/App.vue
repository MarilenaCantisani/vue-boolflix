<template>
  <div id="app">
    <!--//// HEADER -->
    <header>
      <!-- Search-bar -->
      <input placeholder="Cerca qui" type="text" v-model="searchTerm" />
      <button @click="search" type="button">Vai</button>
    </header>
    <!--//// MAIN -->
    <main>
      <!-- Search results movies -->
      <ul v-for="movie in movies" :key="movie.id">
        MOVIES
        <li>Titolo: {{ movie.title }}</li>
        <li>Titolo Originale: {{ movie.original_title }}</li>
        <li>Lingua: {{ movie.original_language }}</li>
        <li>Voto: {{ movie.vote_average }}</li>
      </ul>
    </main>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "App",
  components: {},
  data() {
    return {
      searchTerm: "",
      movies: [],
      api: {
        baseUrl: "https://api.themoviedb.org/3",
        key: "65c487d37adb6d43703803bbf76ecede",
      },
    };
  },
  methods: {
    search() {
      axios
        .get(
          `${this.api.baseUrl}/search/movie?api_key=${this.api.key}&query=${this.searchTerm}`
        )
        .then((res) => {
          this.movies = res.data.results;
        });
    },
  },
};
</script>

<style lang="scss">
</style>
