<template>
  <div class="search-bar">
    <!-- Search-bar -->
    <input
      type="text"
      placeholder="Cerca..."
      v-model="termSearched"
      @keyup.enter="$emit('searchTerm', termSearched)"
    />
    <button @click="$emit('searchTerm', termSearched)" type="button">
      <i class="fas fa-search"></i>
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

<style scoped lang="scss">
</style>