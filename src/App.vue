<script setup lang="ts">
import { ref } from 'vue';
const nuevaTareaTexto = ref('')

const columns = ref([
  {
    title: 'Por hacer',
    tasks: [
      { id: 1, title: 'Diseñar UI', description: 'Crear wireframes' },
      { id: 2, title: 'Configurar DB', description: 'Crear tablas en PostgreSQL' }
    ]
  },
  {
    title: 'En progreso',
    tasks: [
      { id: 3, title: 'Autenticación', description: 'Implementar Login/Registro' }
    ]
  },
  {
    title: 'Finalizado',
    tasks: []
  }
]);

const log = (event: any): void => {
  console.log('Tarea movida:', event);
};
</script>

<template>
  <input 
  v-model="nuevaTareaTexto" 
  type="text" 
  placeholder="Escribir tarea..." 
></input>

<div class="kanban-board">
    <div v-for="column in columns" :key="column.title" class="kanban-column">
      <h3>{{ column.title }}</h3>
      
      <draggable
        class="drag-area"
        :list="column.tasks"
        group="tasks"
        item-key="id"
        @change="log"
      >
        <template #item="{ element }">
          <div class="kanban-card">
            <h4>{{ element.title }}</h4>
            <p>{{ element.description }}</p>
          </div>
        </template>
      </draggable>
    </div>
  </div>
</template>

<style scoped>
.kanban-board {
  display: flex;
  gap: 20px;
  padding: 20px;
  background-color: #f4f5f7;
  height: 100vh;
}

.kanban-column {
  background-color: #ebecf0;
  border-radius: 8px;
  width: 300px;
  padding: 15px;
  display: flex;
  flex-direction: column;
}

.drag-area {
  min-height: 200px;
  flex-grow: 1;
}

.kanban-card {
  background-color: white;
  padding: 10px;
  margin-bottom: 10px;
  border-radius: 4px;
  box-shadow: 0 1px 3px rgba(0,0,0,0.12);
  cursor: grab;
}

.kanban-card:active {
  cursor: grabbing;
}
</style>
