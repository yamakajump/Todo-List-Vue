<template>
    <li class="list-group-item d-flex justify-content-between align-items-center">
      <div>
        <h5>{{ task.description }}</h5>
        <p>Date de début : {{ task.startDate }}</p>
        <p>Date de fin : {{ task.endDate }}</p>
        <p>État : {{ task.status }}</p>
        <p>Priorité : {{ task.priority }}</p>
      </div>
      <button class="btn btn-danger" @click="deleteTask">Supprimer</button>
    </li>
  </template>
  
  <script setup>
  const props = defineProps(['task']);
  const emit = defineEmits(['delete-task']);
  
  const deleteTask = () => {
    emit('delete-task');
  };
  </script>
  