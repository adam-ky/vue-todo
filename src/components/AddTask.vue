<template>
  <form class="add-form">
    <div class="form-control">
      <label>Task</label>
      <input v-model="text" type="text" name="text" placeholder="Add Task" />
    </div>
    <div class="form-control">
      <label>Day & Time</label>
      <input
        v-model="day"
        type="text"
        name="day"
        placeholder="Add Day & Time"
      />
    </div>
    <div class="form-control form-control-check">
      <label>Set Reminder</label>
      <input v-model="reminder" type="checkbox" name="reminder" />
    </div>
    <input
      @click="addTask"
      type="submit"
      value="Save Task"
      class="btn btn-block"
    />
  </form>
</template>

<script>
import { defineComponent } from "vue";

export default defineComponent({
  name: "AddTask",
  data() {
    return {
      text: "",
      day: "",
      reminder: false,
    };
  },
  methods: {
    addTask(e) {
      e.preventDefault();
      const newTask = {
        text: this.text,
        day: this.day,
        reminder: this.reminder,
      };

      this.text = "";
      this.day = "";
      this.reminder = false;

      this.$emit("add-task", newTask);
    },
  },
  emits: ["add-task"],
});
</script>

<style scoped>
.add-form {
  margin-bottom: 40px;
}

.form-control {
  margin: 20px 0;
}

.form-control label {
  display: block;
}

.form-control input {
  width: 100%;
  height: 40px;
  margin: 5px;
  padding: 3px 7px;
  font-size: 17px;
}

.form-control-check {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.form-control-check label {
  flex: 1;
}

.form-control-check input {
  flex: 2;
  height: 20px;
}
</style>
