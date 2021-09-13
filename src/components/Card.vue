<template>
  <!-- Card template  -->
  <div class="card shadow">
    <!-- Cover list item -->
    <img
      class="cover-image"
      :src="getImage(item.poster_path)"
      :alt="item.title || item.name"
    />
    <ul class="description">
      <!-- Title list item -->
      <li class="lh-base">
        <strong>Titolo: </strong> {{ item.title || item.name }}
      </li>
      <li class="lh-base">
        <strong>Titolo Originale:</strong>
        {{ item.original_title || item.original_name }}
      </li>
      <!-- Language/flag list item -->
      <li lh-base>
        <strong>Lingua:</strong>
        <img
          v-if="languageFlag.includes(item.original_language)"
          :src="getFlag(item.original_language)"
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
        <span v-for="star in 5" :key="star">
          <i
            v-if="star <= getVoteAverage(item.vote_average)"
            class="fas fa-star text-yellow"
          ></i>
          <i v-else class="far fa-star"></i>
        </span>
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
  methods: {
    //// Function that returns the path of the flag image
    getFlag(language) {
      return require(`../assets/${language}.png`);
    },
    //// Function that returns the covers of films/series
    getImage(path) {
      if (!path)
        return `https://www.altavod.com/assets/images/poster-placeholder.png`;
      return `${this.apiImage.baseUrlImage}/${this.apiImage.sizeImage}${path}`;
    },
    //// Function that returns tha vote from 1 to 5 rounded up
    getVoteAverage(number) {
      const vote = number / 2;
      const roundNumber = Math.ceil(vote);
      return roundNumber;
    },
  },
};
</script>

<style scoped lang="scss">
@import "../scss/_vars.scss";
.card {
  cursor: pointer;
  padding: 0;
  margin: 0;
  border: 0;
  .cover-image {
    position: relative;
  }
  .description {
    position: absolute;
    visibility: hidden;
    list-style-type: none;
  }
  &:hover .description {
    visibility: visible;
    background-color: black;
    color: white;
    height: 100%;
    padding: 20px 40px;
    overflow-y: scroll;
  }
}
.text-yellow {
  color: $yellow;
}
</style>