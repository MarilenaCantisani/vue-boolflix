<template>
  <div class="search-bar">
    //// Search-bar
    <input type="text" v-model="termSearched" />
    <button @click="$emit('searchTerm', termSearched)" type="button">
      Cerca
    </button>
  </div>
</template>

<script>
export default {
  name: "Search",
  data() {
    return {
      termSearched: "",
    };
  },
};
</script>

<style>
</style>