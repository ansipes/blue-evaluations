<template>
  <main>
    <a
      href="https://github.com/ansipes/blue-evaluations/tree/main/src/assets/pdf"
    >
      Blue Evaluation PDFs
    </a>
    <evaluation
      v-for="(evaluation, index) in evaluations"
      :key="index"
      :evaluation="evaluation"
    />
  </main>
</template>

<script>
import { ref } from "vue";
import e from "./assets/json/evaluations.json";
import Evaluation from "@/components/Evaluation.vue";

export default {
  name: "App",
  components: {
    Evaluation,
  },
  setup() {
    const evaluations = ref(e);

    return {
      evaluations,
    };
  },
};
</script>

<style>
/* Box sizing rules */
*,
*::before,
*::after {
  box-sizing: border-box;
}

/* Remove default margin */
body,
h1,
h2,
h3,
h4,
p,
figure,
blockquote,
dl,
dd {
  margin: 0;
}

/* Remove list styles on ul, ol elements with a list role, which suggests default styling will be removed */
ul[role="list"],
ol[role="list"] {
  list-style: none;
}

/* Set core root defaults */
html:focus-within {
  scroll-behavior: smooth;
}

/* Set core body defaults */
body {
  min-height: 100vh;
  text-rendering: optimizeSpeed;
  line-height: 1.5;
}

/* A elements that don't have a class get default styles */
a:not([class]) {
  text-decoration-skip-ink: auto;
}

/* Make images easier to work with */
img,
picture {
  max-width: 100%;
  display: block;
}

/* Inherit fonts for inputs and buttons */
input,
button,
textarea,
select {
  font: inherit;
}

/* Remove all animations, transitions and smooth scroll for people that prefer not to see them */
@media (prefers-reduced-motion: reduce) {
  html:focus-within {
    scroll-behavior: auto;
  }

  *,
  *::before,
  *::after {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
    scroll-behavior: auto !important;
  }
}

main > article {
  max-width: 50em;
  margin: auto;
}

table,
th,
td {
  border: 1px solid black;
  text-align: center;
}

th,
td {
  padding: 0 0.5rem;
}
</style>
