<template>
  <div class="container">
    <div class="tasks_container" v-for="day in days" :key="day.id">
      <div v-if="day.tasks.length">
        <tasks-list
          @sort="sort"
          @change_priority="changePriority"
          @delete_todo="deleteTodo"
          @delete_day="deleteDay"
          :id-day="day.id"
          :day-name="day.name"
          :task-list="day.tasks"
        ></tasks-list>
      </div>
    </div>
  </div>
</template>
<script setup>
import TasksList from './TasksList.vue'

defineProps({ days: Array })

const emit = defineEmits(['sort', 'change_priority', 'delete_day', 'delete_task'])

function sort(idDay) {
  emit('sort', idDay)
}

function deleteTodo(idDay, idTask) {
  emit('delete_task', idDay, idTask)
}

function deleteDay(idDay) {
  emit('delete_day', idDay)
}

function changePriority(idTask, idDay) {
  emit('change_priority', idTask, idDay)
}
</script>

<style scoped>
.column {
  display: flex;
  gap: 20px;
}
</style>
