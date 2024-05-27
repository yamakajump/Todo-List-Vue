<script setup>
import AddTaskForm from './components/AddTaskForm.vue';
import TaskList from './components/TaskList.vue';
import { ref } from 'vue';

// Liste de tâches réactive
const tasks = ref(JSON.parse(localStorage.getItem('tasks')) || []);

// Fonction pour ajouter une tâche
const addTask = (task) => {
  tasks.value.push(task);
  saveTasks();
};

// Fonction pour supprimer une tâche
const deleteTask = (index) => {
  tasks.value.splice(index, 1);
  saveTasks();
};

// Fonction pour sauvegarder les tâches dans le local storage
const saveTasks = () => {
  localStorage.setItem('tasks', JSON.stringify(tasks.value));
};
</script>

<template>
  <div id="app" class="container">
    <header>
      <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="125" height="125" />
    </header>

    <main>
      <h1 class="my-4">Vue.js ToDo Application</h1>
      <AddTaskForm @add-task="addTask"></AddTaskForm>
      <TaskList :tasks="tasks" @delete-task="deleteTask"></TaskList>
    </main>
  </div>
</template>

<style scoped>
header {
  line-height: 1.5;
  text-align: center;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }
}
</style>
