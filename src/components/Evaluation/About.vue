<template>
  <header>
    <h1>{{ about.course }}</h1>
    <h2>
      {{ about.department }} {{ about.number }}-{{ about.section }}
      {{ about.semester }} {{ about.year }}
    </h2>
    <p>{{ about.instructor }}</p>
    <p>{{ about.received }}/{{ about.audience }}</p>
  </header>
</template>

<script>
export default {
  props: {
    about: {
      type: Object,
      required: true,
    },
  },
};
</script>

<style></style>
