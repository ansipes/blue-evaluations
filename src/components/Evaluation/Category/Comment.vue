<template>
  <article>
    <header>
      <span
        v-for="(tag, index) in comment.tags"
        :key="index"
        :class="getClassFromTag(tag)"
        class="tag"
      >
        {{ tag }}
      </span>
      <span class="date"> {{ comment.semester }} {{ comment.year }} </span>
    </header>
    <section>
      <p v-html="comment.text" />
    </section>
    <footer>
      <a :href="comment.source" target="_blank">Source</a>
      <article v-if="comment.response" class="response">
        <p><strong>Response:</strong></p>
        <p>{{ comment.response }}</p>
      </article>
    </footer>
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

  setup() {
    const getClassFromTag = (tag) => {
      return tag;
    };

    return {
      getClassFromTag,
    };
  },
};
</script>

<style scoped>
article {
  padding: 0 0 1rem 0;
  margin: 2rem 1rem;
  border-radius: 1rem;
  box-shadow: 0 0 0.5rem 0 rgba(0, 0, 0, 0.2);
}

header {
  position: sticky;
  background: rgb(249, 249, 249);
  top: 3.7rem;
  padding: 1rem;
}

section,
footer {
  padding: 0 1rem;
}

span.tag {
  padding: 0.5em 1em;
  margin-right: 0.5em;
  border-radius: 1rem;
  font-size: 0.75rem;
  font-weight: bold;
  color: black;
  background: gray;
}

span.tag.critical {
  background: #fe9c9b;
}

span.tag.positive {
  background: #68ffbe;
}

span.date {
  float: right;
  font-weight: bold;
}

p {
  margin: 1rem 0 1rem 0;
}

p:deep(mark) {
  border-radius: 0.25em;
  padding: 0.05em 0.15em;
  background-color: #fe9c9b;
}

a {
  color: black;
}

.response {
  padding: 0.5em 1em;
  margin: 1em 0 0 0;
  background: rgb(249, 249, 249);
}
</style>
