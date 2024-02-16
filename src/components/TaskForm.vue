<template>
  <div>
    <form class="container form" @submit="HandleAdd($event, name, day, priority)">
      <select class="input day" @change="day = $event.target.value" :value="day" name="" id="">
        <option value="0">ПН</option>
        <option value="1">ВТ</option>
        <option value="2">СР</option>
        <option value="3">ЧТ</option>
        <option value="4">ПТ</option>
        <option value="5">СБ</option>
        <option value="6">ВС</option>
      </select>
      <select
        class="input importanty"
        @change="priority = $event.target.value"
        :value="priority"
        name=""
        id=""
      >
        <option value="true">Важная</option>
        <option value="flase">Не важная</option>
      </select>
      <input class="input text" @change="name = $event.target.value" :value="name" type="text" />
      <input class="submit" type="submit" />
    </form>
  </div>
</template>
<script setup>
let name = ''
let day = 0
let priority = 'true'

const emit = defineEmits(['add'])

function HandleAdd(e, name, dayID, priority) {
  e.preventDefault()

  if (priority == 'true') {
    priority = true
  } else {
    priority = false
  }

  emit('add', parseInt(dayID), { id: Date.now(), name: name, priority: priority })
}
</script>
<style scoped>
.form {
  box-shadow: 0px 4px 4px 0px #00000040;
  border: 1px solid black;
  border-radius: 20px;
  padding: 32px 62px;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  column-gap: 34px;
  row-gap: 24px;
  grid-template-rows: repeat(2, 45px);
  background-color: white;
  margin-top: 80px;
  margin-bottom: 45px;
}

.input {
  border: 1px solid black;
  outline: none;
  padding: 7px 17px;
  font-size: 20px;
  font-weight: 400;
}

.day {
  grid-column: 1;
}

.importanty {
  grid-column: 2;
}

.text {
  grid-column: 1/3;
  grid-row: 2;
}

.submit {
  grid-column: 4;
  grid-row: 2;
  border: 1px solid black;
  border-radius: 23px;
  background-color: #1abc9c;
  color: white;
}
</style>
