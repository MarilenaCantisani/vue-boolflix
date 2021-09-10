<template>
  <div id="app">
    <!--//// HEADER -->
    <header>
      <Search @searchTerm="search" />
    </header>
    <!--//// MAIN -->
    <main>
      <!-- Search results movies -->
      <ul v-for="movie in movies" :key="movie.id">
        <li>Titolo: {{ movie.title }}</li>
        <li>Titolo Originale: {{ movie.original_title }}</li>
        <li>Lingua: {{ movie.original_language }}</li>
        <li>Voto: {{ movie.vote_average }}</li>
      </ul>
    </main>
  </div>
</template>

<script>
import Search from "@/components/Search.vue";
import axios from "axios";
export default {
  name: "App",
  components: {
    Search,
  },
  data() {
    return {
      movies: [],
      api: {
        baseUrl: "https://api.themoviedb.org/3",
        key: "65c487d37adb6d43703803bbf76ecede",
      },
    };
  },
  methods: {
    search(term) {
      axios
        .get(
          `${this.api.baseUrl}/search/movie?api_key=${this.api.key}&query=${term}`
        )
        .then((res) => {
          console.log(res.data.results);
          this.movies = res.data.results;
        });
    },
  },
};
</script>

<style lang="scss">
</style>
