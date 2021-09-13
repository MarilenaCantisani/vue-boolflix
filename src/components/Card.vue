<template>
  <!-- Card template  -->
  <ul>
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
</template>

<script>
export default {
  name: "Card",
  props: ["item"],
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
      if (!path)
        return `https://www.altavod.com/assets/images/poster-placeholder.png`;
      return `${this.apiImage.baseUrlImage}/${this.apiImage.sizeImage}${path}`;
    },
  },
};
</script>

<style>
</style>