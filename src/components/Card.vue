<template>
  <!-- Card template  -->
  <div class="card shadow">
    <!-- Cover list item -->
    <img class="cover-image" :src="image" :alt="title" />
    <ul class="description">
      <!-- Title list item -->
      <li class="lh-base"><strong>Titolo: </strong> {{ title }}</li>
      <li class="lh-base">
        <strong>Titolo Originale:</strong>
        {{ item.original_title || item.original_name }}
      </li>
      <!-- Language/flag list item -->
      <li lh-base>
        <strong>Lingua:</strong>
        <img
          v-if="languageFlag.includes(item.original_language)"
          :src="flag"
          :alt="item.original_language"
          width="20"
          height="12"
          class="mx-2"
        />
        <span v-else class="mx-2 text-uppercase">{{
          item.original_language
        }}</span>
      </li>
      <!-- Star list item -->
      <li class="text-center lh-lg my-3">
        <i
          v-for="star in 5"
          :key="star"
          :class="star <= voteAverage ? 'fas' : 'far'"
          class="fa-star text-yellow"
        ></i>
      </li>
      <!-- Overview list item -->
      <li class="fst-italic">{{ item.overview }}</li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "Card",
  props: ["item"],
  data() {
    return {
      languageFlag: ["it", "en"],
      //* Api images
      apiImage: {
        baseUrlImage: "https://image.tmdb.org/t/p",
        sizeImage: "w342",
      },
    };
  },
  computed: {
    //// Movies/series title
    title() {
      return this.item.title || this.item.name;
    },
    //// Path of the flag image
    flag() {
      return require(`../assets/${this.item.original_language}.png`);
    },
    //// Covers of films/series
    image() {
      if (!this.item.poster_path)
        return `https://www.altavod.com/assets/images/poster-placeholder.png`;
      return `${this.apiImage.baseUrlImage}/${this.apiImage.sizeImage}${this.item.poster_path}`;
    },
    //// Vote from 1 to 5 rounded up
    voteAverage() {
      return Math.ceil(this.item.vote_average / 2);
    },
  },
};
</script>

<style scoped lang="scss">
@import "../scss/_vars.scss";
@import "../scss/cardStyle.scss";
</style>