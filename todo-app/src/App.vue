<script setup>
import { ref, onMounted, watch } from 'vue'

const tasks = ref([])
const newTask = ref('')

// Load tasks from local storage on mount
onMounted(() => {
  const saved = localStorage.getItem('vue-todo-tasks')
  if (saved) {
    try {
      tasks.value = JSON.parse(saved)
    } catch (e) {
      console.error('Failed to parse tasks from local storage', e)
      tasks.value = []
    }
  }
})

// Deep watch tasks to persist any change (adding, deleting, toggling)
watch(
  tasks,
  (newTasks) => {
    localStorage.setItem('vue-todo-tasks', JSON.stringify(newTasks))
  },
  { deep: true }
)

const addTask = () => {
  const text = newTask.value.trim()
  if (text) {
    tasks.value.push({
      id: crypto.randomUUID(),
      text,
      completed: false
    })
    newTask.value = ''
  }
}

const toggleTask = (id) => {
  const task = tasks.value.find(t => t.id === id)
  if (task) {
    task.completed = !task.completed
  }
}

const deleteTask = (id) => {
  tasks.value = tasks.value.filter(t => t.id !== id)
}
</script>

<template>
  <div class="app-wrapper">
    <div class="todo-container">
      <h1>My Tasks</h1>
      
      <form @submit.prevent="addTask" class="input-group">
        <input 
          v-model="newTask" 
          type="text" 
          placeholder="What needs to be done?" 
          class="todo-input"
        />
        <button type="submit" class="add-button">
          <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><line x1="12" y1="5" x2="12" y2="19"></line><line x1="5" y1="12" x2="19" y2="12"></line></svg>
        </button>
      </form>

      <div class="task-list">
        <transition-group name="list">
          <div 
            v-for="task in tasks" 
            :key="task.id" 
            class="task-item" 
            :class="{ completed: task.completed }"
          >
            <div class="task-content" @click="toggleTask(task.id)">
              <div class="checkbox">
                <svg v-if="task.completed" xmlns="http://www.w3.org/2000/svg" width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="3" stroke-linecap="round" stroke-linejoin="round"><polyline points="20 6 9 17 4 12"></polyline></svg>
              </div>
              <span class="task-text">{{ task.text }}</span>
            </div>
            
            <button @click="deleteTask(task.id)" class="delete-button" aria-label="Delete Task">
              <svg xmlns="http://www.w3.org/2000/svg" width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M3 6h18"></path><path d="M19 6v14a2 2 0 0 1-2 2H7a2 2 0 0 1-2-2V6m3 0V4a2 2 0 0 1 2-2h4a2 2 0 0 1 2 2v2"></path><line x1="10" y1="11" x2="10" y2="17"></line><line x1="14" y1="11" x2="14" y2="17"></line></svg>
            </button>
          </div>
        </transition-group>
        
        <div v-if="tasks.length === 0" class="empty-state">
          You have no tasks yet. Add one above!
        </div>
      </div>
    </div>
  </div>
</template>
