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
  <div id="app" class="container my-4">
    <header class="text-center mb-4">
      <h1 class="display-4 text-primary">Todo List Now !</h1>
    </header>

    <main>
      <AddTaskForm @add-task="addTask"></AddTaskForm>
      <TaskList :tasks="tasks" @delete-task="deleteTask"></TaskList>
    </main>

    <footer class="text-center py-3">
      Réalisé par BATARD Corentin et BASOL Nathan
    </footer>
  </div>
</template>

<style scoped>
header {
  line-height: 1.5;
}
footer {
  background-color: #f8f9fa;
  color: #6c757d;
  font-size: 14px;
}
</style>
