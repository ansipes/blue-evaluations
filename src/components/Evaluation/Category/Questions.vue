<template>
  <section>
    <question
      v-for="(question, index) in questions"
      :key="index"
      :index="index"
      :question="question"
    />
  </section>
</template>

<script>
import Question from "@/components/Evaluation/Category/Question.vue";

export default {
  components: {
    Question,
  },
  props: {
    questions: {
      type: Array,
      required: true,
    },
  },
};
</script>

<style></style>
