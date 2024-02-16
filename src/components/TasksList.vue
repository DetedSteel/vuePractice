<template>
  <div class="day_container" @mouseenter="show" @mouseleave="hide">
    <h2 class="day_name">{{ dayName }}</h2>
    <div class="tasks">
      <div
        @mouseenter="hide"
        @mouseleave="show"
        v-for="task in taskList"
        :key="task.id"
        :class="`task ${task.priority ? 'red' : 'green'}`"
      >
        <h3 class="task_text" @click="changePriority(idDay, task.id)">
          {{ task.name }}
        </h3>
        <button @click="emit('delete_todo', idDay, task.id)" class="delete"></button>
      </div>
    </div>
  </div>
  <button
    @mouseenter="show"
    @mouseleave="hide"
    @click="emit('delete_day', idDay)"
    :class="`delete_day ${isShow ? '' : 'none'}`"
  ></button>
</template>
<script setup>
import { ref } from 'vue'

defineProps({
  taskList: Array,
  dayName: String,
  idDay: Number
})

const emit = defineEmits(['sort', 'change_priority', 'delete_todo', 'delete_day'])

function changePriority(idDay, idTask) {
  emit('change_priority', idTask, idDay)
  emit('sort', idDay)
}

let isShow = ref(false)

const show = () => {
  isShow.value = true
}

const hide = () => {
  isShow.value = false
}
</script>
<style scoped>
.day_name {
  background-color: #34495e;
  color: white;
  font-size: 30px;
  font-weight: 400;
  height: inherit;
  padding: 13px 16px;
  display: flex;
  align-items: center;
  width: 80px;
}

.task:hover .delete_day {
  display: none;
}

.task_text {
  color: white;
  font-weight: 400;
  font-size: 30px;
  max-width: 252px;
}

.red {
  background-color: #e74c3c;
}

.green {
  background-color: #1abc9c;
}

.tasks {
  width: 100%;
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  column-gap: 17px;
  row-gap: 15px;
  background-color: white;
  padding: 11px 24px;
}

.none {
  display: none !important;
}
</style>
