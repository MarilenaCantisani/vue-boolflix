<template>
  <section class="search-result">
    <!-- Search results movies -->
    <ul v-for="item in list" :key="item.id">
      <li>Titolo: {{ item.title || item.name }}</li>
      <li>Titolo Originale: {{ item.original_title || item.original_name }}</li>
      <li>
        Lingua:
        <img
          v-if="languageFlag.includes(item.original_language)"
          :src="getFlag(item.original_language)"
          :alt="item.original_language"
          width="20"
          height="12"
        />
        <span v-else>Lingua: {{ item.original_language }}</span>
      </li>
      <li>Voto: {{ item.vote_average }}</li>
      <li>
        <img :src="getImage(item.poster_path)" :alt="item.title || item.name" />
      </li>
    </ul>
  </section>
</template>

<script>
export default {
  name: "ResultList",
  props: ["list"],
  data() {
    return {
      languageFlag: ["it", "en"],
      apiImage: {
        baseUrlImage: "https://image.tmdb.org/t/p",
        sizeImage: "w342",
      },
    };
  },
  computed: {
    imageUrl() {
      return `${this.apiImage.baseUrlImage}/${this.apiImage.sizeImage}${this.item.poster_path}`;
    },
  },
  methods: {
    getFlag(language) {
      return require(`../assets/${language}.png`);
    },
    getImage(path) {
      return `${this.apiImage.baseUrlImage}/${this.apiImage.sizeImage}${path}`;
    },
  },
};
</script>

<style>
</style>

