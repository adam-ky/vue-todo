<template>
  <header>
    <h1>{{ title }}</h1>
    <Button
      v-show="showButton"
      @on-click="toggleShowAddTask"
      :color="showAddTask ? 'red' : 'green'"
      :text="showAddTask ? 'Close' : 'Add Task'"
    />
  </header>
</template>

<script>
import Button from "./Button.vue";

export default {
  name: "AppHeader",
  props: {
    showAddTask: Boolean,
    title: String,
  },
  components: {
    Button,
  },
  methods: {
    toggleShowAddTask() {
      this.$emit("toggle-show-add-task");
    },
  },
  computed: {
    showButton() {
      return this.$route.path === "/";
    },
  },
  emits: ["toggle-show-add-task"],
};
</script>

<style scoped>
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
}
</style>
