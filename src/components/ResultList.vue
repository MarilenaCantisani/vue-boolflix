<template>
  <section class="search-result">
    //// Search results movies
    <div v-if="type === 'movies'">
      <ul v-for="item in list" :key="item.id">
        <li>Titolo: {{ item.title }}</li>
        <li>Titolo Originale: {{ item.original_title }}</li>
        <li v-if="languageFlag.includes(item.original_language)">
          Lingua:
          <img
            :src="language(item.original_language)"
            alt="item.original_language"
            width="20"
            height="12"
          />
        </li>
        <li v-else>Lingua: {{ item.original_language }}</li>
        <li>Voto: {{ item.vote_average }}</li>
      </ul>
    </div>

    //// Search results movies
    <div v-else>
      <ul v-for="item in list" :key="item.id">
        <li>Titolo: {{ item.name }}</li>
        <li>Titolo Originale: {{ item.original_name }}</li>
        <li v-if="languageFlag.includes(item.original_language)">
          Lingua:
          <img
            :src="language(item.original_language)"
            alt="item.original_language"
            width="20"
            height="12"
          />
        </li>
        <li v-else>Lingua: {{ item.original_language }}</li>
        <li>Voto: {{ item.vote_average }}</li>
      </ul>
    </div>
  </section>
</template>

<script>
export default {
  name: "ResultList",
  props: ["list", "type"],
  data() {
    return {
      languageFlag: ["it", "en"],
    };
  },
  methods: {
    language(text) {
      return require(`../assets/${text}.png`);
    },
  },
};
</script>

<style>
</style>

