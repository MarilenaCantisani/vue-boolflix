<template>
  <div id="app">
    <!-- HEADER -->
    <header>
      <Search @searchTerm="search" />
    </header>
    <!-- MAIN -->
    <main>
      <!-- Results search movies -->
      <ResultList :list="movies" />
      <!-- Results search series -->
      <ResultList :list="series" />
    </main>
  </div>
</template>

<script>
import Search from "@/components/Search.vue";
import ResultList from "@/components/ResultList.vue";
import axios from "axios";
export default {
  name: "App",
  components: {
    Search,
    ResultList,
  },
  data() {
    return {
      //* Filtered array of movies and tv series
      movies: [],
      series: [],
      //* My API key
      api: {
        baseUrl: "https://api.themoviedb.org/3",
        key: "65c487d37adb6d43703803bbf76ecede",
      },
    };
  },
  methods: {
    search(query) {
      if (!query) {
        this.movies = this.series = [];
        return;
      }
      //// Fetch movies list
      this.fetchApi(query, "search/movie", "movies");
      //// Fetch series list
      this.fetchApi(query, "search/tv", "series");
    },
    fetchApi(query, endpoint, entity) {
      axios
        .get(
          `${this.api.baseUrl}/${endpoint}?api_key=${this.api.key}&query=${query}`
        )
        .then((res) => {
          console.log(res.data.results);
          this[entity] = res.data.results;
        })
        .catch((err) => {
          console.log(err);
        });
    },
  },
};
</script>

<style lang="scss">
</style>
