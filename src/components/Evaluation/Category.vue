<template>
  <section>
    <h1>{{ category.title }}</h1>
    <questions :questions="category.questions" />
    <comments :comments="category.comments" />
  </section>
</template>

<script>
import Questions from "@/components/Evaluation/Category/Questions.vue";
import Comments from "@/components/Evaluation/Category/Comments.vue";

export default {
  components: {
    Questions,
    Comments,
  },
  props: {
    category: {
      type: Object,
      required: true,
    },
  },
};
</script>

<style></style>
