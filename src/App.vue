<script setup>
import { ref, computed } from 'vue'

// Initialize Value
let id = 0
const dataToDo = ref([{id: id++, todo: 'eat', complete: false}, {id: id++, todo: "coding", complete: true}, {id: id++, todo: "sleep", complete: false}])

// Add To Do
const inputAdd = ref('')
const addToDo = () => {
  dataToDo.value.push({id: id++, todo: inputAdd.value, complete: false})
  inputAdd.value = ""
}

// Edit To Do
// const isEdit = ref(false)
const toggleEdit = (data) => {
  // isEdit.value = !isEdit.value
  inputEdit.value = data.todo
  inputEditChange.value = inputEdit.value
}
const inputEdit = ref('')

const inputEditChange = ref('')
const editToDo = data => {
  dataToDo.value.forEach(val => val.id == data.id ? val.todo = inputEditChange.value : false)
}

// Delete To Do
const deleteToDo = data => {
  dataToDo.value = dataToDo.value.filter(ele => ele.id !== data.id)
}

// Computed Filter
const showedToDo = computed(() => {
  return showAll.value ? dataToDo.value : (showToDo.value ? dataToDo.value.filter(ele => !ele.complete) : showCompleted.value ? dataToDo.value.filter(ele => ele.complete) : false)
})

// Filter Button
// Show All
const showAll = ref(true)
const toggleShowAll = () => {
  showAll.value = true
  showToDo.value = false
  showCompleted.value = false
}

// // Show To Do
const showToDo = ref(false)
const toggleShowToDo = () => {
  showAll.value = false
  showToDo.value = true
  showCompleted.value = false
}

// // Show Completed
const showCompleted = ref(false)
const toggleShowCompleted = () => {
  showAll.value = false
  showToDo.value = false
  showCompleted.value = true
}
</script>

<template>
  <div class="flex flex-col items-center bg-black text-white h-full">
    <div class="text-6xl my-12 text-blue-800">
      <h1 class="font-bold">To Do List</h1>
    </div>
    <input class="text-2xl rounded-md text-slate-700 p-2" type="text" placeholder="Input To Do" v-model="inputAdd" @keyup.enter="addToDo">

    <div class="w-1/2 bg-slate-800 mt-10 py-6 rounded-xl">
      <ul class="list-inside hover:list-inside">
        <li v-for="data in showedToDo" :key="data.id" class="flex m-4">
          <input class="basis-1/4" type="checkbox" v-model="data.complete">
          <div class="basis-1/2" @dblclick="toggleEdit(data)">
            <input v-if="data.todo === inputEdit" type="text" v-model="inputEditChange" @vue:mounted="({ el }) => el.focus()" @keyup.enter="editToDo(data)" class="text-xl font-bold rounded-md text-slate-700">
            <label v-else for="" class="text-xl font-bold">
              {{ data.todo }}
            </label>
          </div>
          <div class="basis-1">
            <button class="bg-red-800 rounded-xl p-2" @click="deleteToDo(data)">Delete</button>
          </div>
          
        </li>
      </ul>
    </div>
  <footer class="flex gap-8 mt-8 bg-slate-600 p-4 text-gray-700 rounded-lg">
    <button class="bg-white rounded-md p-2" @click="toggleShowAll" :class="{ 'bg-blue-400': showAll }">Show All</button>
    <button class="bg-white rounded-md p-2" @click="toggleShowToDo" :class="{ 'bg-blue-400': showToDo }">Show To Do</button>
    <button class="bg-white rounded-md p-2" @click="toggleShowCompleted" :class="{ 'bg-blue-400': showCompleted }">Show Complete</button>
  </footer>
  </div>
</template>

<style scoped>

</style>
