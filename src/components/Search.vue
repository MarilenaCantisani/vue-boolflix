<template>
  <div class="search-results">
    <!-- Search results -->
    <ul v-for="movie in movies" :key="movie.id">
      <li>Titolo: {{ movie.title }}</li>
      <li>Titolo Originale: {{ movie.original_title }}</li>
      <li>Lingua: {{ movie.original_language }}</li>
      <li>Voto: {{ movie.vote_average }}</li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "Search",
  props: ["movies"],
};
</script>

<style>
</style>