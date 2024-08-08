<script setup>
import { reactive, ref } from "vue";

import TaskList from "@/components/TaskList.vue";

let tasks = ref(JSON.parse(localStorage.getItem("tasks")) || []);
// let completedTasks = ref(
//   JSON.parse(localStorage.getItem("completedTasks")) || []
// );

const current_task = reactive({
  task_id: 0,
  task_name: "",
  description: "",
  task_complete: false,
  due_date: new Date(),
});
function createTask() {
  current_task.task_id = tasks.value.length + 1;
  // console.log(current_task.task_id);
  tasks.value.push({ ...current_task });
  localStorage.setItem("tasks", JSON.stringify(tasks.value));
}
function toggle_task(task_id) {
  // console.log(typeof task_id);
  // console.log(tasks.value[task_id - 1]);
  tasks.value[task_id - 1].task_complete =
    !tasks.value[task_id - 1].task_complete;
  // console.log(tasks.value[task_id - 1]);
  localStorage.setItem("tasks", JSON.stringify(tasks.value));
  // tasks = ref(localStorage.getItem("tasks", JSON.parse(tasks.value)));
  // console.log(tasks.value[task_id - 1]);
  // console.log(tasks.value[task_id - 1].task);
}
</script>

<template>
  <div class="todo-container">
    <form class="todoForm" @submit.prevent="createTask">
      <h3 class="title-of-list">ADD new Task</h3>
      <div class="text-input">
        <label for="">Task Name:</label>
        <input type="text" v-model="current_task.task_name" />
      </div>
      <div class="text-input">
        <label for="">Description:</label>
        <textarea type="text" v-model="current_task.description"></textarea>
      </div>
      <div class="text-input">
        <label for="">Due Date:</label>
        <input
          type="date"
          name="task-completion-date"
          v-model="current_task.due_date"
        />
      </div>
      <button type="submit">Add Task</button>
    </form>
    <TaskList
      :tasks="tasks"
      @task_toggle="toggle_task"
      :type="false"
    ></TaskList>
    <TaskList :tasks="tasks" @task_toggle="toggle_task" :type="true"></TaskList>
  </div>
</template>
<style scoped>
.text-input {
  display: flex;
  flex-direction: column;
  gap: 0.3em;
  padding-bottom: 0.5em;
}
</style>
