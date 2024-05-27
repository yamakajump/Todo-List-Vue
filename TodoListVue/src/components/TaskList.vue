<template>
    <div>
      <div class="filters mb-4">
        <button class="btn btn-secondary mr-2" @click="filterTasks('all')">Toutes</button>
        <button class="btn btn-secondary mr-2" @click="filterTasks('À faire')">À faire</button>
        <button class="btn btn-secondary mr-2" @click="filterTasks('En cours')">En cours</button>
        <button class="btn btn-secondary mr-2" @click="filterTasks('Terminé')">Terminé</button>
        <button class="btn btn-secondary mr-2" @click="sortTasks('priority')">Priorité</button>
        <button class="btn btn-secondary mr-2" @click="sortTasks('startDate')">Date de début</button>
        <button class="btn btn-secondary" @click="sortTasks('endDate')">Date de fin</button>
      </div>
      <ul class="list-group">
        <TaskItem 
          v-for="(task, index) in filteredTasks" 
          :key="index" 
          :task="task"
          @delete-task="deleteTask(index)"
        ></TaskItem>
      </ul>
    </div>
  </template>
  
  <script setup>
  import TaskItem from './TaskItem.vue';
  import { ref, watch } from 'vue';
  
  const props = defineProps(['tasks']);
  const emit = defineEmits(['delete-task']);
  
  const filteredTasks = ref(props.tasks);
  
  watch(
    () => props.tasks,
    (newTasks) => {
      filteredTasks.value = newTasks;
    },
    { deep: true }
  );
  
  const filterTasks = (status) => {
    if (status === 'all') {
      filteredTasks.value = props.tasks;
    } else {
      filteredTasks.value = props.tasks.filter(task => task.status === status);
    }
  };
  
  const sortTasks = (criteria) => {
    filteredTasks.value.sort((a, b) => a[criteria].localeCompare(b[criteria]));
  };
  
  const deleteTask = (index) => {
    emit('delete-task', index);
  };
  </script>
  