<script setup>
import { ref } from 'vue'

// Initialize Value
let id = 0
const dataToDo = ref([{id: id++, todo: 'eat', complete: false}, {id: id++, todo: "coding", complete: true}])

// Add To Do
const inputAdd = ref('asdasd')
const addToDo = () => {
  dataToDo.value.push({id: id++, todo: inputAdd.value, complete: false})
  inputAdd.value = ""
}

// Edit To Do
const isEdit = ref(false)
const toggleEdit = () => {
  isEdit.value = !isEdit.value
}
const inputEdit = ref('')
const editToDo = data => {
  
}
</script>

<template>
  <div class="flex flex-col items-center bg-black text-white h-full">
    <div class="text-6xl my-5 text-blue-800">
      <h1 class="font-bold">To Do List</h1>
      {{ dataToDo }}
    </div>
    <input class="text-2xl rounded-md text-slate-700" type="text" placeholder="Input To Do" v-model="inputAdd" @keyup.enter="addToDo">

    <div class="w-1/2 bg-slate-800 mt-10 p-4 rounded-xl">
      <table class="w-full text-left">
        <thead>
          <tr>
            <th>Check All</th>
            <th>To Do</th>
            <th>Delete</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="data in dataToDo" :key="data.id">
            <td>
              <input type="checkbox" v-model="data.complete">
            </td>
            <td @dblclick="toggleEdit">
              <p v-if="!isEdit" class="font-bold text-md">{{ data.todo }}</p>
              <input v-else class="text-md rounded-md text-slate-700" type="text" v-model="data.todo" @keyup.enter="editToDo(data)">
            </td>
            <td>
              <button>delete</button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  <footer class="flex gap-8 mt-8 bg-slate-600 p-4 text-gray-700 rounded-lg">
    <button class="bg-white rounded-md p-2">Show All</button>
    <button class="bg-white rounded-md p-2">Show To Do</button>
    <button class="bg-white rounded-md p-2">Show Complete</button>
  </footer>
  </div>
</template>

<style scoped>

</style>
