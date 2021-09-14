<template>
  <!-- Search results -->
  <section class="row">
    <h2>{{ title }}</h2>
    <div
      v-for="item in list"
      :key="item.id"
      class="col-xs-12 col-md-4 col-lg-3 card-template"
    >
      <!-- Card component -->
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
  props: ["list", "title"],
};
</script>

<style scoped lang="scss">
h2 {
  margin-top: 20px;
  padding-left: 20px;
  font-weight: bolder;
}
</style>

