<script setup>
import { ref } from 'vue'
import TaskForm from './components/TaskForm.vue'
import TasksOfDay from './components/TasksOfDay.vue'

const days = ref([
  { id: 0, name: 'ПН', tasks: [] },
  { id: 1, name: 'ВТ', tasks: [] },
  { id: 2, name: 'СР', tasks: [] },
  { id: 3, name: 'ЧТ', tasks: [] },
  { id: 4, name: 'ПТ', tasks: [] },
  { id: 5, name: 'СБ', tasks: [] },
  { id: 6, name: 'ВС', tasks: [] }
])

function addTask(id, task) {
  days.value = days.value.map((e) => {
    if (e.id === id) {
      e.tasks.push(task)
    }
    return e
  })
  sort(id)
}

function changePriority(idTask, idDay) {
  days.value = days.value.map((e) => {
    if (e.id === idDay) {
      e.tasks.map((i) => {
        if (i.id === idTask) {
          i.priority = !i.priority
        }
        return e
      })
    }
    return e
  })
}

function sort(id) {
  days.value = days.value.map((e) => {
    if (e.id === id) {
      e.tasks.sort((c, n) => {
        if (n.priority && c.priority) {
          return 0
        } else if (n.priority && !c.priority) {
          return 1
        } else {
          return -1
        }
      })
    }
    return e
  })
}

function deleteTodo(idDay, idTask) {
  days.value = days.value.map((e) => {
    if (e.id === idDay) {
      e.tasks = e.tasks.filter((t) => t.id !== idTask)
    }
    return e
  })
}

function deleteAll(id) {
  days.value = days.value.filter((e) => {
    if (e.id === id) {
      e.tasks = e.tasks.splice(e.tasks.length)
    }
    return e
  })
}
</script>

<template>
  <div>
    <task-form @add="addTask"></task-form>
    <tasks-of-day
      @delete_day="deleteAll"
      @delete_task="deleteTodo"
      @change_priority="changePriority"
      @sort="sort"
      :days="days"
    ></tasks-of-day>
  </div>
</template>

<style scoped></style>
