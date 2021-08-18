<template>
  <article>
    <about :about="evaluation.about" />
    <category
      v-for="(section, index) in evaluation.sections"
      :key="index"
      :category="section"
    />
  </article>
</template>

<script>
import About from "@/components/Evaluation/About.vue";
import Category from "@/components/Evaluation/Category.vue";

export default {
  components: {
    About,
    Category,
  },
  props: {
    evaluation: {
      type: Object,
      required: true,
    },
  },
};
</script>

<style></style>
