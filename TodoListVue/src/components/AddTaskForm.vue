<template>
    <form @submit.prevent="submitForm">
      <div class="form-group">
        <label for="description">Description</label>
        <input type="text" class="form-control" v-model="description" required>
      </div>
      <div class="form-group">
        <label for="startDate">Date de début</label>
        <input type="date" class="form-control" v-model="startDate" required>
      </div>
      <div class="form-group">
        <label for="endDate">Date de fin</label>
        <input type="date" class="form-control" v-model="endDate" required>
      </div>
      <div class="form-group">
        <label for="status">État</label>
        <select class="form-control" v-model="status" required>
          <option>À faire</option>
          <option>En cours</option>
          <option>Terminé</option>
        </select>
      </div>
      <div class="form-group">
        <label for="priority">Priorité</label>
        <select class="form-control" v-model="priority" required>
          <option>Haute</option>
          <option>Moyenne</option>
          <option>Basse</option>
        </select>
      </div>
      <button type="submit" class="btn btn-primary">Ajouter la tâche</button>
    </form>
  </template>
  
  <script setup>
  import { ref } from 'vue';
  
  const description = ref('');
  const startDate = ref('');
  const endDate = ref('');
  const status = ref('À faire');
  const priority = ref('Moyenne');
  
  const emit = defineEmits(['add-task']);
  
  const submitForm = () => {
    const newTask = {
      description: description.value,
      startDate: startDate.value,
      endDate: endDate.value,
      status: status.value,
      priority: priority.value
    };
    emit('add-task', newTask);
    description.value = '';
    startDate.value = '';
    endDate.value = '';
    status.value = 'À faire';
    priority.value = 'Moyenne';
  };
  </script>
  