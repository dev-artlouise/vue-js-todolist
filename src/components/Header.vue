<template>
  <header>
    <h1>{{ title }}</h1>
    <Button
      @btn-click="$emit('toggle-add-task')"
      :text="showAddTask ? 'Close' : 'Add Task'"
      :color="showAddTask ? 'red' : 'green'"
    />
    <!-- Reuse components with different props -->
    <!-- <Button text="Update Task" color="Blue" />
    <Button text="Delete Task" color="red" /> -->
  </header>
</template>

<script>
import Button from "./Button";

export default {
  name: "Header",

  //normal implementation
  // props: {
  //   title: String,
  // },

  //With Default Value
  props: {
    title: {
      type: String,
      default: "Hello World",
    },
    showAddTask: Boolean,
  },

  components: {
    Button,
  },
};
</script>

<style scoped>
Header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-top: 20px;
}
</style>