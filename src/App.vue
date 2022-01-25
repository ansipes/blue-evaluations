<template>
  <main>
    <div style="padding: 1rem; text-align: center">
      <p>Instructor Reviews</p>
      <h1>Andrew Sipes</h1>
      <p>
        <a href="#about" title="Learn more about why I made this.">About</a> |
        <a href="#faq" title="Answers to frequently asked questions.">FAQs</a> |
        <a
          href="https://forms.office.com/r/BS87veDUt4"
          title="Make suggestions to help me improve the UX/UI."
          target="_blank"
        >
          Feedback
        </a>
      </p>
      <div style="display: flex; justify-content: center">
        <section class="average instructor">
          <h2>{{ instructor }}</h2>
          <strong>Instructor</strong>
        </section>
        <section class="average course">
          <h2>{{ course }}</h2>
          <strong>Course</strong>
        </section>
      </div>
    </div>

    <header>
      <section>
        <button
          :class="{ active: filter === 'all' }"
          @click.prevent="filter = 'all'"
        >
          All
        </button>
        <button
          :class="{ active: filter === 'positive' }"
          @click.prevent="filter = 'positive'"
        >
          Positive
        </button>
        <button
          :class="{ active: filter === 'critical' }"
          @click.prevent="filter = 'critical'"
        >
          Critical
        </button>
      </section>

      <select v-model.number="sort">
        <option value="1">Newest</option>
        <option value="0">Oldest</option>
      </select>
    </header>

    <comments :comments="comments" />

    <div id="about" style="padding: 1rem">
      <h1>About</h1>
      <p>Hi, my name is Andrew.</p>
      <p>
        I teach MEJO 187, Foundations of Interactive Media. This page features
        feedback from the following semesters:
      </p>
      <ul>
        <li>Fall 2019</li>
        <li>Spring 2020</li>
        <li>Fall 2020</li>
        <li>Spring 2021</li>
      </ul>
      <h2>Comments</h2>
      <p>Using the utility bar, you can filter by tag and sort by date.</p>
      <p>I have tagged comments with the following labels:</p>
      <ul>
        <li>positive (46)</li>
        <li>critical (14)</li>
      </ul>
      <p>
        Some comments feature both positive and critical tags. For ease of use,
        I have marked the critical portions of these comments.
      </p>
      <p>
        I respond to some comments to detail steps I have taken to improve the
        adminstration of the course and my effectiveness as an instructor.
      </p>

      <h3 id="faq">Frequently Asked Questions</h3>
      <dl>
        <dt>Why did you make this?</dt>
        <dd>
          <ul>
            <li>
              I value transparency. I believe students should be able to make
              informed decisions about taking a course with a given instructor.
            </li>
            <li>
              There are no public ratings for me on sites like
              <a href="https://www.ratemyprofessors.com/" target="_blank">
                Rate My Professors</a
              >.
            </li>
            <li>
              The vast majority of my Fall 2021 students (13/15) said this
              information would be helpful.
            </li>
            <li>
              I also want to illustrate to current and prospective students that
              I value their feedback and am more than willing to adjust my
              teaching style accordingly.
            </li>
          </ul>
        </dd>
        <dt>Did you get permission to do this?</dt>
        <dd>
          <p>Yes.</p>
          <p>I confirmed this was permissable by contacting:</p>
          <ul>
            <li>
              <a
                href="http://hussman.unc.edu/directory/faculty/ca-tuggle"
                target="_blank"
              >
                Senior Associate Dean for Undergraduate Studies
              </a>
            </li>
            <li>
              <a
                href="https://curricula.unc.edu/course-evaluations/"
                target="_blank"
              >
                <abbr title="College of Arts &amp; Sciences">CAS</abbr>
                Evaluations
              </a>
            </li>
            <li>
              <a
                href="https://universitycounsel.unc.edu/staff/kristen-lewis/"
                target="_blank"
              >
                University Counsel
              </a>
            </li>
          </ul>
          <p>This is the guidance I received:</p>
          <ul>
            <li>
              I must audit free response fields and redact any
              <a
                href="https://studentprivacy.ed.gov/content/personally-identifiable-information-education-records"
                target="_blank"
                >Personally Identifiable Information</a
              >
            </li>
            <li>
              I must not publish groups of response data with a participant size
              that is less than or equal to 5
            </li>
          </ul>
        </dd>
        <dt>Did you omit any data?</dt>
        <dd>
          <p>Yes.</p>
          <p>
            I taught Summer Session II 2021, but I only had two students. Per
            University Counsel, I cannot release datasets with a participant
            size that is less than or equal to 5.
          </p>
          <p>
            Not all of the data is displayed on this page, but you are welcome
            to
            <a
              href="https://github.com/ansipes/blue-evaluations/tree/main/src/assets/pdf"
              target="_blank"
            >
              view the original reports</a
            >.
          </p>
        </dd>
        <dt>Do you plan to improve this site?</dt>
        <dd>
          <p>
            Definitely! If you are interested in seeing my plans, requesting a
            feature, or filing a bug, please
            <a
              href="https://github.com/ansipes/blue-evaluations"
              target="_blank"
            >
              visit the repository</a
            >. You can also
            <a href="https://forms.office.com/r/BS87veDUt4" target="_blank"
              >leave a suggestion using the feedback form</a
            >.
          </p>
        </dd>
        <dt>Are you becoming a better instructor?</dt>
        <dd>
          <p>Yes! Spring 2021 was my best semester so far.</p>
          <p>
            I plan to update this site with charts that illustrate my progress.
            If you would like to see that data now, please
            <a
              href="https://github.com/ansipes/blue-evaluations/tree/main/src/assets/pdf"
              target="_blank"
            >
              view the original reports</a
            >.
          </p>
        </dd>
      </dl>
    </div>
  </main>
  <button v-show="totop" @click="top" id="totop" title="Go to top">Top</button>
</template>

<script>
import { ref, computed } from "vue";
import e from "./assets/json/evaluations.json";
import Comments from "@/components/Evaluation/Category/Comments.vue";

export default {
  name: "App",
  components: {
    Comments,
  },
  setup() {
    const evaluations = ref(e);
    const sort = ref(1);
    const filter = ref("all");

    const course = computed(() => {
      let responses = [];

      evaluations.value.forEach((evaluation) => {
        evaluation.sections.forEach((section) => {
          let overall = section.questions.find(
            (question) => question.flag === "course"
          );
          if (overall) {
            responses = responses.concat(overall.responses);
          }
        });
      });

      let totals = {};

      responses.forEach((response) => {
        totals[response.label] =
          typeof totals[response.label] === "number"
            ? totals[response.label] + response.value
            : response.value;
      });

      let count = Object.values(totals).reduce(
        (accumulator, currentValue) => accumulator + currentValue
      );

      let weights = {};

      weights["Excellent"] = totals.Excellent * 5;
      weights["Above Average"] = totals["Above Average"] * 4;
      weights["Average"] = totals["Average"] * 3;
      weights["Below Average"] = totals["Below Average"] * 2;
      weights["Poor"] = totals["Below Average"] * 1;

      let weightedTotal = Object.values(weights).reduce(
        (accumulator, currentValue) => accumulator + currentValue
      );

      return (weightedTotal / count).toFixed(1);
    });

    const instructor = computed(() => {
      let responses = [];

      evaluations.value.forEach((evaluation) => {
        evaluation.sections.forEach((section) => {
          let overall = section.questions.find(
            (question) => question.flag === "instructor"
          );
          if (overall) {
            responses = responses.concat(overall.responses);
          }
        });
      });

      let totals = {};

      responses.forEach((response) => {
        totals[response.label] =
          typeof totals[response.label] === "number"
            ? totals[response.label] + response.value
            : response.value;
      });

      let count = Object.values(totals).reduce(
        (accumulator, currentValue) => accumulator + currentValue
      );

      let weights = {};

      weights["Excellent"] = totals.Excellent * 5;
      weights["Above Average"] = totals["Above Average"] * 4;
      weights["Average"] = totals["Average"] * 3;
      weights["Below Average"] = totals["Below Average"] * 2;
      weights["Poor"] = totals["Below Average"] * 1;

      let weightedTotal = Object.values(weights).reduce(
        (accumulator, currentValue) => accumulator + currentValue
      );

      console.log(weightedTotal, count);
      return (weightedTotal / count).toFixed(1);
    });

    const comments = computed(() => {
      let comments = [];
      evaluations.value.forEach((evaluation) => {
        evaluation.sections.forEach((section) => {
          comments = comments.concat(
            section.comments.map((comment) => {
              comment.date = new Date(
                `${evaluation.about.year}-${
                  evaluation.about.semester === "Fall" ? "12" : "05"
                }-10`
              );
              comment.year = evaluation.about.year;
              comment.semester = evaluation.about.semester;
              comment.source = `https://github.com/ansipes/blue-evaluations/blob/main/src/assets/pdf/mejo-187-00${
                evaluation.about.section
              }-${evaluation.about.semester.toLowerCase()}-${
                evaluation.about.year
              }.pdf`;
              return comment;
            })
          );
        });
      });

      return comments
        .filter((comment) => {
          if (filter.value === "all") {
            return true;
          }

          if (
            filter.value === "critical" &&
            comment.tags.includes("critical")
          ) {
            return true;
          }

          if (
            filter.value === "positive" &&
            comment.tags.includes("positive")
          ) {
            return true;
          }
        })
        .sort((a, b) => {
          if (sort.value) {
            return b.date - a.date;
          }
          return a.date - b.date;
        });
    });

    const totop = ref(false);

    window.onscroll = function () {
      scrollFunction();
    };

    function scrollFunction() {
      if (
        document.body.scrollTop > 20 ||
        document.documentElement.scrollTop > 20
      ) {
        totop.value = true;
      } else {
        totop.value = false;
      }
    }

    function top() {
      document.body.scrollTop = 0;
      document.documentElement.scrollTop = 0;
    }

    return {
      filter,
      sort,
      course,
      instructor,
      comments,
      totop,
      top,
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

html {
  font-family: sans-serif;
  line-height: 1.5;
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

main {
  margin: 0 auto;
  max-width: 75ch;
}

main > header {
  padding: 1rem;
  display: flex;
  justify-content: space-between;
  position: sticky;
  top: 0;
  background: #4b9cd3;
  z-index: 1;
  /* border-bottom-left-radius: 0.5rem;
  border-bottom-right-radius: 0.5rem; */
}

main > header button {
  margin-right: 0.25em;
}

.average {
  padding: 0.5em 1em;
  text-align: center;
  font-size: 0.75rem;
  border-radius: 0.5em;
  min-width: 5rem;
  margin: 1em 1em 0 0;
}

.average.course,
.average.instructor {
  background: #68ffbe;
}

button,
select {
  border-radius: 0.25em;
  border: 0.05em solid white;
}

button.active {
  background: #13294b;
  color: white;
}

dt {
  margin-top: 1em;
  font-weight: bold;
}

ul {
  padding-left: 1em;
  margin: 0.5em 0 0.5em 0;
}

ul li {
  margin: 0.5em 0;
}

#about p {
  margin: 0.75em 0;
}

#totop {
  display: block;
  position: fixed;
  bottom: 20px;
  right: 30px;
  z-index: 99;
  font-size: 18px;
  border: none;
  outline: none;
  background-color: black;
  color: white;
  cursor: pointer;
  padding: 15px;
  border-radius: 4px;
}
</style>
