<template>
  <article>
    <p>
      <span v-for="(tag, index) in comment.tags" :key="index">
        {{ tag }}
      </span>
    </p>
    <p>{{ comment.text }}</p>
  </article>
</template>

<script>
export default {
  props: {
    comment: {
      type: Object,
      required: true,
    },
  },
};
</script>

<style></style>
