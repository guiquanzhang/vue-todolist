<template>
  <div class="todo-container">
    <TodoHeader />
    <TodoInput @add-todo="addTodo" />
    <TodoStats 
      :total="todos.length"
      :completed="completedCount"
      :remaining="remainingCount"
    />
    <ul class="todo-list">
      <TodoItem
        v-for="todo in filteredTodos"
        :key="todo.id"
        :todo="todo"
        @delete="deleteTodo(todo.id)"
        @update:todo="updateTodo"
      />
    </ul>
    <TodoFilter v-model="currentFilter" />
  </div>
</template>

<script setup name="TodoList">
import { ref, computed } from 'vue'
import TodoHeader from './TodoHeader.vue'
import TodoInput from './TodoInput.vue'
import TodoStats from './TodoStats.vue'
import TodoItem from './TodoItem.vue'
import TodoFilter from './TodoFilter.vue'

const todos = ref([])
const currentFilter = ref('all')

const completedCount = computed(() => {
  return todos.value.filter(todo => todo.completed).length
})

const remainingCount = computed(() => {
  return todos.value.filter(todo => !todo.completed).length
})

const filteredTodos = computed(() => {
  switch (currentFilter.value) {
    case 'active':
      return todos.value.filter(todo => !todo.completed)
    case 'completed':
      return todos.value.filter(todo => todo.completed)
    default:
      return todos.value
  }
})

const addTodo = (text) => {
  todos.value.push({
    id: Date.now(),
    text,
    completed: false
  })
  saveTodos()
}

const deleteTodo = (id) => {
  todos.value = todos.value.filter(todo => todo.id !== id)
  saveTodos()
}

const updateTodo = (updatedTodo) => {
  const index = todos.value.findIndex(todo => todo.id === updatedTodo.id)
  if (index !== -1) {
    todos.value[index] = updatedTodo
    saveTodos()
  }
}

const saveTodos = () => {
  localStorage.setItem('todos', JSON.stringify(todos.value))
}

// 从localStorage加载数据
const loadTodos = () => {
  const savedTodos = localStorage.getItem('todos')
  if (savedTodos) {
    todos.value = JSON.parse(savedTodos)
  }
}

loadTodos()
</script>

<style scoped>
.todo-container {
  max-width: 800px;
  width: 100%;
  background: rgba(255, 255, 255, 0.9);
  backdrop-filter: blur(10px);
  border-radius: 20px;
  padding: 30px;
  box-shadow: 0 8px 32px rgba(31, 38, 135, 0.15);
  border: 1px solid rgba(255, 255, 255, 0.18);
}

.todo-list {
  list-style: none;
  padding: 0;
  margin: 20px 0;
}

h1 {
  color: #1a365d;
  font-size: 2.5rem;
  margin-bottom: 30px;
  font-weight: 600;
  text-align: center;
}
</style> 