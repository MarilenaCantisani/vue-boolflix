<template>
  <div id="app">
    <!--//// HEADER -->
    <header>
      <Search @searchTerm="search" />
    </header>
    <!--//// MAIN -->
    <main>
      <ResultList :list="movies" :type="typeMovie" />
      <hr />
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
      typeMovie: "movies",
      typeSeries: "series",
      movies: [],
      series: [],
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
