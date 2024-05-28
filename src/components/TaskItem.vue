<template>
  <li class="list-group-item d-flex justify-content-between align-items-center mb-2 p-3 border rounded shadow-sm">
    <div>
      <h5 class="mb-1">{{ task.description }}</h5>
      <small>Date de début : {{ task.startDate }}</small><br>
      <small>Date de fin : {{ task.endDate }}</small><br>
      <small>État : {{ task.status }}</small><br>
      <small>Priorité : {{ task.priority }}</small>
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
