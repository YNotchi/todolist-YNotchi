<script setup lang="ts">
import { ref } from 'vue'

interface Task {
  con: string
  ena: boolean //true:未完、false:完了
}

const tasks = ref<Task[]>([])
const newTaskCon = ref('')
const newTaskEna = ref(true)

const addTask = () => {
  if(newTaskCon.value != ''){
    tasks.value.push({ con: newTaskCon.value, ena: newTaskEna.value })
    newTaskCon.value = ''
    newTaskEna.value = true
  }
}

const compTask = (taskCon: string) => {
    tasks.value = tasks.value.map((task) => {
      if(task.con == taskCon){
        task.ena = false
      }
      return task
    })
}
</script>

<template>
  <div>
    <div>
      <h2>unfinished</h2>
      <ul>
        <div v-for="task in tasks" :key="task.con">
          <div v-if="task.ena == true">  
            <li> 
                <button @click="compTask(task.con)">fin</button>
                {{ task.con }}
            </li>
          </div>
        </div>
      </ul>
    </div>
    <div>
      <h2>finished</h2>
      <ul>
        <div v-for="task in tasks" :key="task.con">
          <div v-if="task.ena == false">  
            <li> {{ task.con }}</li>
          </div>
        </div>
      </ul>
    </div>
    <div>
      <label>
        Task
        <input v-model="newTaskCon" type="text" />
      </label>
      <button @click="addTask">add</button>
    </div>
  </div>
</template>

<style>
.over500 {
  color: red;
}
</style>