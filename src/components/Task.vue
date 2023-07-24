<template>
  <div
    @dblclick="$emit('toggle-reminder')"
    :class="[task.reminder ? 'reminder' : '', 'task']"
    v-if="task"
  >
    <h3>
      {{ task.text }}
      <i @click="$emit('delete-task')" class="fas fa-times"></i>
    </h3>
    <p>{{ task.day }}</p>
  </div>
</template>

<script lang="ts">
import { PropType, defineComponent } from "vue";
import { Task } from "../utils/types";

export default defineComponent({
  name: "TaskItem",
  props: {
    task: Object as PropType<Task>,
  },
  emits: ["toggle-reminder", "delete-task"],
});
</script>

<style scope>
.fas {
  color: red;
}

.task {
  background: #f4f4f4;
  margin: 5px;
  padding: 10px 20px;
  cursor: pointer;
}
.task.reminder {
  border-left: 5px solid green;
}
.task h3 {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
</style>
