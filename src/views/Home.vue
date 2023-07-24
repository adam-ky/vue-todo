<template>
  <AddTask v-show="showAddTask" @add-task="addTask" />
  <Tasks
    @toggle-reminder="toggleReminder"
    @delete-task="deleteTask"
    :tasks="tasks"
  />
</template>

<script lang="ts">
import { defineComponent } from "vue";
import Tasks from "../components/Tasks.vue";
import AddTask from "../components/AddTask.vue";
import { Task } from "../utils/types";

export default defineComponent({
  name: "HomePage",
  components: {
    Tasks,
    AddTask,
  },
  props: {
    showAddTask: Boolean,
  },
  data() {
    return {
      tasks: [] as Task[],
    };
  },
  methods: {
    async deleteTask(id: number) {
      if (confirm("Are you sure?")) {
        try {
          const response = await fetch(`api/tasks/${id}`, {
            method: "delete",
          });

          if (response.status === 200) {
            this.tasks = this.tasks.filter(task => task.id !== id);
          }
        } catch (err) {
          console.error("Error deleting task", err);
        }
      }
    },
    async toggleReminder(id: number) {
      try {
        const taskToUpdate = await this.fetchTask(id);
        const updatedTask = {
          ...taskToUpdate,
          reminder: !taskToUpdate.reminder,
        };

        const response = await fetch(`api/tasks/${id}`, {
          method: "put",
          headers: {
            "Content-Type": "application/json",
          },
          body: JSON.stringify(updatedTask),
        });

        if (response.status === 200) {
          const data = await response.json();

          this.tasks = this.tasks.map(task =>
            task.id === id ? { ...task, reminder: data.reminder } : task
          );
        }
      } catch (err) {
        console.error("Error deleting task", err);
      }
    },
    async addTask(task: Task) {
      try {
        const response = await fetch("api/tasks", {
          method: "post",
          headers: {
            "Content-Type": "application/json",
          },
          body: JSON.stringify(task),
        });

        const newTask = await response.json();

        this.tasks = [...this.tasks, newTask];
      } catch (err) {
        console.error("Error adding new task", err);
      }
    },
    async fetchTasks() {
      return await fetch("api/tasks").then(response => response.json());
    },
    async fetchTask(id: number) {
      return await fetch(`api/tasks/${id}`).then(response => response.json());
    },
  },
  async created() {
    this.tasks = await this.fetchTasks();
  },
});
</script>
