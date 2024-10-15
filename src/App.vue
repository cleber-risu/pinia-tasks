<script setup>
import { ref } from 'vue';

import { useTaskStore } from './stores/TaskStore';
import TaskDetails from './components/TaskDetails.vue';
import TaskForm from './components/TaskForm.vue';

const taskStore = useTaskStore()

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

    <!-- loading -->
    <div class="loading" v-if="taskStore.isLoading">
      Loading Tasks...
    </div>

    <!-- new task form -->
     <div class="new-task-form">
      <TaskForm />
     </div>

    <!-- filter -->
    <nav class="filter">
      <button @click="filter = 'all'">All tasks</button>
      <button @click="filter = 'favs'">Fav tasks</button>
    </nav>

    <!-- task list -->
    <div class="task-list" v-if="filter === 'all'">
      <p>You have <strong>{{ taskStore.totalCount }}</strong> tasks left to do</p>
      <div v-for="task in taskStore.tasks" :key="task.id">
        <TaskDetails :task="task" />
      </div>
    </div>
     
    <div class="task-list" v-if="filter === 'favs'">
      <p>You have <strong>{{ taskStore.favCount }}</strong> tasks left to do</p>
      <div v-for="task in taskStore.favs" :key="task.id">
        <TaskDetails :task="task" />
      </div>
    </div>
  </main>
</template>

<style scoped>

</style>
