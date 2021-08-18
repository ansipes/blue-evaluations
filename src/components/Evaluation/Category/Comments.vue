<template>
  <section>
    <comment
      v-for="(comment, index) in comments"
      :key="index"
      :comment="comment"
    />
  </section>
</template>

<script>
import Comment from "@/components/Evaluation/Category/Comment.vue";

export default {
  components: {
    Comment,
  },
  props: {
    comments: {
      type: Array,
      required: true,
    },
  },
};
</script>

<style></style>
