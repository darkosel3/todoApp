<script setup>
import { computed } from "vue";

const props = defineProps({
  tasks: Array,
  type: Boolean,
  title: String,
});
const emit = defineEmits(["task_toggle"]);
const title = computed(() => {
  return props.type == true ? "Completed" : "Task";
});
const filteredTasks = computed(() => {
  return props.tasks.filter((task) => task.task_complete == props.type);
});
</script>

<template>
  <div class="list-of-tasks">
    <h3 class="title-of-list">{{ title }} List</h3>
    <ul>
      <li class="task" v-for="task in filteredTasks" :key="task.task_id">
        <div class="task-div" v-show="task.task_complete == type">
          <input
            type="checkbox"
            @click="$emit('task_toggle', task.task_id)"
            :checked="task.task_complete"
          />
          <div class="text">
            <p class="task-name">
              <router-link
                style="text-decoration: none; color: inherit"
                :to="'/task/' + task.task_id"
                >{{ task.task_name }}</router-link
              >
            </p>
            <p>{{ task.due_date }}</p>
          </div>
        </div>
      </li>
    </ul>
  </div>
</template>
