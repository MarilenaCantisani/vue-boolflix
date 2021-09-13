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
    <li>
      <span v-for="star in 5" :key="star">
        <i
          v-if="star <= getVoteAverage(item.vote_average)"
          class="fas fa-star"
        ></i>
        <i v-else class="far fa-star"></i>
      </span>
    </li>
    <li>Overview: {{ item.overview }}</li>
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
  methods: {
    getFlag(language) {
      return require(`../assets/${language}.png`);
    },
    getImage(path) {
      if (!path)
        return `https://www.altavod.com/assets/images/poster-placeholder.png`;
      return `${this.apiImage.baseUrlImage}/${this.apiImage.sizeImage}${path}`;
    },
    getVoteAverage(number) {
      const vote = number / 2;
      const roundNumber = Math.ceil(vote);
      return roundNumber;
    },
  },
};
</script>

<style>
</style>