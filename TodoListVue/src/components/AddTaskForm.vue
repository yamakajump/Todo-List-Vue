<template>
  <form @submit.prevent="submitForm" class="mb-4 p-4 border rounded shadow-sm bg-light">
    <div class="form-group mb-3">
      <label for="description">Description</label>
      <input type="text" class="form-control" v-model="description" required>
    </div>
    <div class="form-group mb-3">
      <label for="startDate">Date de début</label>
      <input type="date" class="form-control" v-model="startDate" :min="today" required>
    </div>
    <div class="form-group mb-3">
      <label for="endDate">Date de fin</label>
      <input type="date" class="form-control" v-model="endDate" :min="today" required>
    </div>
    <div class="form-group mb-3">
      <label for="status">État</label>
      <select class="form-control" v-model="status" required>
        <option>À faire</option>
        <option>En cours</option>
        <option>Terminé</option>
      </select>
    </div>
    <div class="form-group mb-3">
      <label for="priority">Priorité</label>
      <select class="form-control" v-model="priority" required>
        <option>Haute</option>
        <option>Moyenne</option>
        <option>Basse</option>
      </select>
    </div>
    <button type="submit" class="btn btn-primary btn-block">Ajouter la tâche</button>
    <div v-if="errorMessage" class="alert alert-danger mt-3">
      {{ errorMessage }}
    </div>
  </form>
</template>

<script setup>
import { ref } from 'vue';

const description = ref('');
const today = new Date().toISOString().split('T')[0]; // Date du jour au format YYYY-MM-DD
const startDate = ref('');
const endDate = ref('');
const status = ref('À faire');
const priority = ref('Moyenne');
const errorMessage = ref('');

const emit = defineEmits(['add-task']);

const submitForm = () => {
  if (!description.value.trim()) {
    errorMessage.value = 'Veuillez saisir une description.';
    return;
  }

  if (new Date(startDate.value) > new Date(endDate.value)) {
    errorMessage.value = 'La date de fin ne peut pas être antérieure à la date de début.';
    return;
  }

  const newTask = {
    description: description.value,
    startDate: startDate.value,
    endDate: endDate.value,
    status: status.value,
    priority: priority.value
  };
  emit('add-task', newTask);

  // Réinitialiser le formulaire
  description.value = '';
  startDate.value = '';
  endDate.value = '';
  status.value = 'À faire';
  priority.value = 'Moyenne';
  errorMessage.value = '';
};
</script>
