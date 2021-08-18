<template>
  <main>
    <a
      href="https://github.com/ansipes/blue-evaluations/tree/main/src/assets/pdf"
    >
      Blue Evaluation PDFs
    </a>
    <article v-for="(evaluation, index) in evaluations" :key="index">
      <h1>{{ evaluation.about.course }}</h1>
      <h2>
        {{ evaluation.about.department }} {{ evaluation.about.number }}-{{
          evaluation.about.section
        }}
        {{ evaluation.about.semester }} {{ evaluation.about.year }}
      </h2>
      <p>{{ evaluation.about.instructor }}</p>
      <p>{{ evaluation.about.received }}/{{ evaluation.about.audience }}</p>
      <section v-for="(section, index) in evaluation.sections" :key="index">
        <h1>{{ section.title }}</h1>
        <article v-for="(question, index) in section.questions" :key="index">
          <h1>{{ index + 1 }}. {{ question.title }}</h1>
          <table>
            <thead>
              <th>Course</th>
              <th>School</th>
            </thead>
            <tbody>
              <tr>
                <td>{{ question.course.mean }}</td>
                <td>{{ question.school.mean }}</td>
              </tr>
              <tr>
                <td>{{ question.course.median }}</td>
                <td>{{ question.school.median }}</td>
              </tr>
              <tr>
                <td>{{ question.course.standardDeviation }}</td>
                <td>{{ question.school.standardDeviation }}</td>
              </tr>
            </tbody>
          </table>
        </article>
        <article v-for="(comment, index) in section.comments" :key="index">
          <p>
            <span v-for="(tag, index) in comment.tags" :key="index">
              {{ tag }}
            </span>
          </p>
          <p>{{ comment.text }}</p>
        </article>
      </section>
    </article>
  </main>
</template>

<script>
import { ref } from "vue";
import e from "./assets/json/evaluations.json";

export default {
  name: "App",
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
