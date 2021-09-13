<template>
  <section class="search-result">
    <!-- Search results movies -->
    <div v-for="item in list" :key="item.id">
      <Card :item="item" />
    </div>
  </section>
</template>

<script>
import Card from "@/components/Card.vue";
export default {
  name: "ResultList",
  components: {
    Card,
  },
  props: ["list"],
};
</script>

<style>
</style>

