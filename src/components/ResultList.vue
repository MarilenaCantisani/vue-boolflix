<template>
  <section class="search-result row">
    <!-- Search results movies -->
    <div
      v-for="item in list"
      :key="item.id"
      class="col-xs-12 col-md-4 col-lg-3 card-template"
    >
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
.card-template {
  padding: 20px;
}
</style>

