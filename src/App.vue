<script setup>
import { ref } from 'vue';
import { storeToRefs } from 'pinia';

import { useTaskStore } from './stores/TaskStore';
import TaskDetails from './components/TaskDetails.vue';
import TaskForm from './components/TaskForm.vue';

const taskStore = useTaskStore()

const { tasks, isLoading, favs, totalCount, favCount } = storeToRefs(taskStore)

// fetch tasks
taskStore.getTasks()

const filter = ref('all')
</script>

<template>
  <main>
    <!-- heading -->
    <header>
      <img src="./assets/pinia-logo.svg" alt="Pinia logo" />
      <h1>Pinia tasks</h1>
    </header>

    <!-- new task form -->
     <div class="new-task-form">
      <TaskForm />
     </div>

    <!-- filter -->
    <nav class="filter">
      <button @click="filter = 'all'">All tasks</button>
      <button @click="filter = 'favs'">Fav tasks</button>
    </nav>

    <!-- loading -->
    <div class="loading" v-if="isLoading">
      Loading Tasks...
    </div>

    <!-- task list -->
    <div class="task-list" v-if="filter === 'all'">
      <p>You have <strong>{{ totalCount }}</strong> tasks left to do</p>
      <div v-for="task in tasks" :key="task.id">
        <TaskDetails :task="task" />
      </div>
    </div>
     
    <div class="task-list" v-if="filter === 'favs'">
      <p>You have <strong>{{ favCount }}</strong> tasks left to do</p>
      <div v-for="task in favs" :key="task.id">
        <TaskDetails :task="task" />
      </div>
    </div>

    <!--
      <button @click="taskStore.$reset">Reset</button>
    -->
  </main>
</template>

<style scoped>

</style>
