<template>
  <div>
    <div class="filters mb-4">
      <h3>Afficher les tâches</h3>
      <button class="btn btn-secondary mr-2 mb-2" @click="setFilter('all')">Toutes</button>
      <button class="btn btn-secondary mr-2 mb-2" @click="setFilter('À faire')">À faire</button>
      <button class="btn btn-secondary mr-2 mb-2" @click="setFilter('En cours')">En cours</button>
      <button class="btn btn-secondary mr-2 mb-2" @click="setFilter('Terminé')">Terminé</button>
    </div>
    <div class="filters mb-4">
      <h3>Filtrer les tâches</h3>
      <button class="btn btn-secondary mr-2 mb-2" @click="setSort('priority')">Priorité</button>
      <button class="btn btn-secondary mr-2 mb-2" @click="setSort('startDate')">Date de début</button>
      <button class="btn btn-secondary mb-2" @click="setSort('endDate')">Date de fin</button>
    </div>
    <ul class="list-group">
      <TaskItem 
        v-for="(task, index) in displayedTasks" 
        :key="index" 
        :task="task"
        @delete-task="deleteTask(index)"
      ></TaskItem>
    </ul>
  </div>
</template>

<script setup>
import { ref, watch, computed } from 'vue';
import TaskItem from './TaskItem.vue';

const props = defineProps(['tasks']);
const emit = defineEmits(['delete-task']);

const filter = ref('all');
const sortCriteria = ref('');

const setFilter = (newFilter) => {
  filter.value = newFilter;
};

const setSort = (criteria) => {
  sortCriteria.value = criteria;
};

const sortedTasks = computed(() => {
  let tasksCopy = [...props.tasks];

  if (sortCriteria.value === 'priority') {
    tasksCopy.sort((a, b) => {
      const priorities = { 'Haute': 3, 'Moyenne': 2, 'Basse': 1 };
      return priorities[b.priority] - priorities[a.priority] || new Date(a.endDate) - new Date(b.endDate);
    });
  } else if (sortCriteria.value === 'startDate') {
    tasksCopy.sort((a, b) => new Date(a.startDate) - new Date(b.startDate));
  } else if (sortCriteria.value === 'endDate') {
    tasksCopy.sort((a, b) => new Date(a.endDate) - new Date(b.endDate));
  }

  return tasksCopy;
});

const displayedTasks = computed(() => {
  if (filter.value === 'all') {
    return sortedTasks.value;
  } else {
    return sortedTasks.value.filter(task => task.status === filter.value);
  }
});

const deleteTask = (index) => {
  emit('delete-task', index);
};
</script>

<style scoped>
.filters .btn {
  margin-bottom: 0.5rem;
}
.filters h3 {
  margin-bottom: 1rem;
  margin-top: 1rem;
}
</style>
