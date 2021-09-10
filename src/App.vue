<template>
  <div id="app">
    //// HEADER
    <header>
      <Search @searchTerm="search" />
    </header>
    //// MAIN
    <main>
      <!-- Results search movies -->
      <ResultList :list="movies" :type="typeMovie" />
      <!-- Results search series -->
      <ResultList :list="series" :type="typeSeries" />
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
      //* Type to pass as parameters
      typeMovie: "movies",
      typeSeries: "series",
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
    search(term) {
      //// Call axios to movies
      axios
        .get(
          `${this.api.baseUrl}/search/movie?api_key=${this.api.key}&query=${term}`
        )
        .then((res) => {
          console.log(res.data.results);
          this.movies = res.data.results;
        });
      //// Call axios to the series
      axios
        .get(
          `${this.api.baseUrl}/search/tv?api_key=${this.api.key}&query=${term}`
        )
        .then((res) => {
          console.log(res.data.results);
          this.series = res.data.results;
        });
    },
  },
};
</script>

<style lang="scss">
</style>
