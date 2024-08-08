<script setup>
import { useRoute } from "vue-router";
import { ref } from "vue";
const route = useRoute();
const taskID = Number(route.params.id);
let tasks = JSON.parse(localStorage.getItem("tasks"));
let task = ref(tasks[taskID - 1]);
console.log(task);
</script>

<template>
  <div>{{ task }}</div>
</template>
