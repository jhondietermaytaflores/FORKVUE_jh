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
const progressPercentage = computed(() => {
  if (totalTasks.value === 0) return 0
  return Math.round((completedTasks.value / totalTasks.value) * 100)
})
</script>

<template>
  <div class="container">
    <header class="header">
      <h1>Sistema de Gestión de Tareas</h1>
    </header>

    <h1> Desarrollado por Jhon D. Mayta Flores</h1>

    <!-- Formulario para agregar una nueva tarea -->
    <form @submit.prevent="addTask" class="task-form">
      <input v-model="newTaskText" type="text" placeholder="Escribe una nueva tarea..." class="task-input" />
      <button type="submit" class="btn btn-add">Agregar</button>
    </form>

    <p> DESDE RAMA:feat/seg-funcion ioasjfdisjfiajokdsaoidjaoisjdaiosjdaiosjdoa</p>

    <!-- Resumen y estadísticas de tareas -->
    <div class="stats-bar">
      <span><strong>Total de tareas:</strong> {{ totalTasks }}</span>
      <span><strong>Completadas:</strong> {{ completedTasks }} de {{ totalTasks }}</span>
    </div>

    <p>1ra
      Lorem ipsum dolor sit amet consectetur adipisicing elit. Harum ab eveniet pariatur explicabo repellat sit ex ad,
      in inventore blanditiis quas, nisi fugit sint facilis adipisci illum magnam aliquid! Molestiae?</p>

    <!-- Mensaje cuando la lista de tareas está vacía -->
    <div v-if="tasks.length === 0" class="empty-message">
      <p>No hay tareas registradas. ¡Agrega la primera!</p>
    </div>

    <!-- Lista de tareas -->
    <ul v-else class="task-list">
      <li v-for="task in tasks" :key="task.id" class="task-item" :class="{ completed: task.completed }">
        <label class="task-content">
          <div class="app-layout">
            <div class="container">
              <!-- Encabezado atractivo -->
              <header class="header">
                <div class="header-badge">
                  <svg class="badge-icon" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none"
                    stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                    <polyline points="9 11 12 14 22 4"></polyline>
                    <path d="M21 12v7a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V5a2 2 0 0 1 2-2h11"></path>
                  </svg>
                  <span>Gestión Diaria</span>
                </div>
                <h1 class="header-title">Sistema de Gestión de Tareas</h1>
                <p class="header-subtitle">Organiza tus prioridades, mantén el enfoque y completa tus objetivos.</p>
              </header>

              <!-- Formulario para agregar una nueva tarea -->
              <form @submit.prevent="addTask" class="task-form">
                <div class="input-container">
                  <svg class="input-icon" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none"
                    stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                    <circle cx="12" cy="12" r="10"></circle>
                    <line x1="12" y1="8" x2="12" y2="16"></line>
                    <line x1="8" y1="12" x2="16" y2="12"></line>
                  </svg>
                  <input v-model="newTaskText" type="text" placeholder="¿Qué tarea tienes pendiente hoy?..."
                    class="task-input" />
                </div>
                <button type="submit" class="btn btn-add" :disabled="!newTaskText.trim()">
                  <svg class="btn-icon" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none"
                    stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round">
                    <line x1="12" y1="5" x2="12" y2="19"></line>
                    <line x1="5" y1="12" x2="19" y2="12"></line>
                  </svg>
                  <span>Agregar</span>
                </button>
              </form>
            </div>
          </div>
        </label>
      </li>
    </ul>
    <p>
      desde 3r branch
      Lorem ipsum dolor sit amet consectetur adipisicing elit. Hic harum dicta quasi, officiis quam, unde cupiditate
      soluta aperiam vero ipsa accusantium repellat dignissimos fuga iusto? Molestias magnam non iusto tenetur?
    </p>


    <!-- Resumen y estadísticas de tareas -->
    <div class="stats-card">
      <div class="stats-bar">
        <div class="stat-item">
          <span class="stat-dot stat-dot-total"></span>
          <span><strong>Total de tareas:</strong> {{ totalTasks }}</span>
        </div>
        <div class="stat-item">
          <span class="stat-dot stat-dot-completed"></span>
          <span><strong>Completadas:</strong> {{ completedTasks }} de {{ totalTasks }}</span>
        </div>
        <div class="stat-item stat-item-percentage" v-if="totalTasks > 0">
          <span class="stat-percentage-badge">{{ progressPercentage }}% completado</span>
        </div>
      </div>

      <!-- Barra de progreso visual -->
      <div class="progress-track" v-if="totalTasks > 0">
        <div class="progress-fill" :style="{ width: progressPercentage + '%' }"
          :class="{ 'is-completed': progressPercentage === 100 }"></div>
      </div>
    </div>

    <!-- Mensaje cuando la lista de tareas está vacía -->
    <div v-if="tasks.length === 0" class="empty-message">
      <div class="empty-icon-box">
        <svg class="empty-icon" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor"
          stroke-width="1.75" stroke-linecap="round" stroke-linejoin="round">
          <path d="M14 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V8z"></path>
          <polyline points="14 2 14 8 20 8"></polyline>
          <line x1="16" y1="13" x2="8" y2="13"></line>
          <line x1="16" y1="17" x2="8" y2="17"></line>
          <polyline points="10 9 9 9 8 9"></polyline>
        </svg>
      </div>
      <h3 class="empty-title">¡Todo listo por ahora!</h3>
      <p class="empty-description">No hay tareas registradas. ¡Agrega la primera para empezar a organizar tu día!</p>
    </div>

    <!-- Lista de tareas -->
    <ul v-else class="task-list">
      <li v-for="task in tasks" :key="task.id" class="task-item" :class="{ completed: task.completed }">
        <label class="task-content">
          <input type="checkbox" :checked="task.completed" @change="toggleTask(task)" class="task-checkbox" />
          <span class="task-text">{{ task.text }}</span>
        </label>

        <button @click="removeTask(task.id)" class="btn btn-delete" title="Eliminar tarea" aria-label="Eliminar tarea">
          <svg class="btn-delete-icon" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none"
            stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
            <polyline points="3 6 5 6 21 6"></polyline>
            <path d="M19 6v14a2 2 0 0 1-2 2H7a2 2 0 0 1-2-2V6m3 0V4a2 2 0 0 1 2-2h4a2 2 0 0 1 2 2v2"></path>
            <line x1="10" y1="11" x2="10" y2="17"></line>
            <line x1="14" y1="11" x2="14" y2="17"></line>
          </svg>
          <span class="btn-delete-label">Eliminar</span>
        </button>
      </li>
    </ul>

    <!-- Pie informativo sutil -->
    <footer class="footer-info">
      <span>{{ completedTasks === totalTasks && totalTasks > 0 ? '🎉 ¡Felicidades! Has completado todas tus tareas' :
        'Haz clic en la casilla para marcar una tarea como completada' }}</span>
    </footer>
  </div>

</template>
