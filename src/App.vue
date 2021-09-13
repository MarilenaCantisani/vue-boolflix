<template>
  <div id="app">
    <!-- HEADER -->
    <header class="bg-dark">
      <div class="container">
        <h1>BOOLFIX</h1>
        <Search @searchTerm="search" />
      </div>
    </header>
    <!-- MAIN -->
    <main class="bg-secondary">
      <section class="container">
        <!-- Results search movies -->
        <ResultList :list="movies" />
        <!-- Results search series -->
        <ResultList :list="series" />
      </section>
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
@import "./scss/generalStyle.scss";
@import "./scss/headerStyle.scss";
main {
  min-height: 100vh;
  height: 100%;
}
</style>
