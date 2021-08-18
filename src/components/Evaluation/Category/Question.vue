<template>
  <article>
    <h1>
      <span v-if="index !== false">{{ index + 1 }}.</span>
      {{ question.title }}
    </h1>
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
</template>

<script>
export default {
  props: {
    question: {
      type: Object,
      required: true,
    },
    index: {
      type: [Number, Boolean],
      required: false,
      default: false,
    },
  },
};
</script>

<style></style>
