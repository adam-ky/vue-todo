<template>
  <div v-for="task in tasks" :key="task.id">
    <Task
      @toggle-reminder="$emit('toggle-reminder', task.id)"
      @delete-task="$emit('delete-task', task.id)"
      :task="task"
    />
  </div>
</template>

<script lang="ts">
import { PropType } from "vue";
import Task from "./Task.vue";
import { Task as TaskType } from "../utils/types";

export default {
  name: "TaskList",
  props: {
    tasks: Array as PropType<TaskType[]>,
  },
  components: {
    Task,
  },
  emits: ["toggle-reminder", "delete-task"],
};
</script>
