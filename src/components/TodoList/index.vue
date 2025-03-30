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
      />
    </ul>
    <TodoFilter v-model="currentFilter" />
  </div>
</template>

<script setup>
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
  margin: 0 auto;
  padding: 20px;
}

.todo-list {
  list-style: none;
  padding: 0;
  margin: 0;
}
</style> 