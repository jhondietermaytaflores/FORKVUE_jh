<script setup>
import { ref, computed } from 'vue'

// Lista inicial de tareas de ejemplo
const tasks = ref([
  { id: 1, text: 'Aprender conceptos básicos de Git', completed: true },
  { id: 2, text: 'Crear una rama para una nueva funcionalidad', completed: false }
])

// Campo para capturar el texto de la nueva tarea
const newTaskText = ref('')

// Agregar una nueva tarea a la lista
const addTask = () => {
  const text = newTaskText.value.trim()
  if (!text) return

  tasks.value.push({
    id: Date.now(),
    text: text,
    completed: false
  })

  newTaskText.value = ''
}

// Eliminar una tarea según su ID
const removeTask = (id) => {
  tasks.value = tasks.value.filter(task => task.id !== id)
}

// Cambiar el estado de completado de una tarea
const toggleTask = (task) => {
  task.completed = !task.completed
}

// Contadores computados de tareas
const totalTasks = computed(() => tasks.value.length)
const completedTasks = computed(() => tasks.value.filter(t => t.completed).length)
</script>

<template>
  <div class="container">
    <header class="header">
      <h1>Sistema de Gestión de Tareas</h1>
    </header>

    <!-- Formulario para agregar una nueva tarea -->
    <form @submit.prevent="addTask" class="task-form">
      <input
        v-model="newTaskText"
        type="text"
        placeholder="Escribe una nueva tarea..."
        class="task-input"
      />
      <button type="submit" class="btn btn-add">Agregar</button>
    </form>

    <!-- Resumen y estadísticas de tareas -->
    <div class="stats-bar">
      <span><strong>Total de tareas:</strong> {{ totalTasks }}</span>
      <span><strong>Completadas:</strong> {{ completedTasks }} de {{ totalTasks }}</span>
    </div>

    <p>1ra
      Lorem ipsum dolor sit amet consectetur adipisicing elit. Harum ab eveniet pariatur explicabo repellat sit ex ad, in inventore blanditiis quas, nisi fugit sint facilis adipisci illum magnam aliquid! Molestiae?</p>

    <!-- Mensaje cuando la lista de tareas está vacía -->
    <div v-if="tasks.length === 0" class="empty-message">
      <p>No hay tareas registradas. ¡Agrega la primera!</p>
    </div>

    <!-- Lista de tareas -->
    <ul v-else class="task-list">
      <li 
        v-for="task in tasks" 
        :key="task.id" 
        class="task-item"
        :class="{ completed: task.completed }"
      >
        <label class="task-content">
          <input
            type="checkbox"
            :checked="task.completed"
            @change="toggleTask(task)"
            class="task-checkbox"
          />
          <span class="task-text">{{ task.text }}</span>
        </label>
        
        <button 
          @click="removeTask(task.id)" 
          class="btn btn-delete"
          title="Eliminar tarea"
        >
          Eliminar
        </button>
      </li>
    </ul>
  </div>
</template>
