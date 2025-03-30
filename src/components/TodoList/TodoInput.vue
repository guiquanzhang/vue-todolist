<template>
  <div class="todo-input">
    <input 
      v-model="newTodo" 
      @keyup.enter="addTodo"
      placeholder="请输入新的待办事项"
      type="text"
      class="todo-input-field"
    >
    <button @click="addTodo" class="add-button">
      <i class="fas fa-plus"></i> 添加
    </button>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const emit = defineEmits(['add-todo'])
const newTodo = ref('')

const addTodo = () => {
  if (newTodo.value.trim()) {
    emit('add-todo', newTodo.value)
    newTodo.value = ''
  }
}
</script>

<style scoped>
.todo-input {
  display: flex;
  gap: 10px;
  margin-bottom: 20px;
}

.todo-input-field {
  flex: 1;
  padding: 12px;
  border: 2px solid #e9ecef;
  border-radius: 6px;
  font-size: 16px;
  transition: border-color 0.3s ease;
}

.todo-input-field:focus {
  outline: none;
  border-color: #4CAF50;
}

.add-button {
  padding: 12px 24px;
  background-color: #4CAF50;
  color: white;
  border: none;
  border-radius: 6px;
  cursor: pointer;
  font-size: 16px;
  display: flex;
  align-items: center;
  gap: 8px;
  transition: all 0.3s ease;
}

.add-button:hover {
  background-color: #45a049;
  transform: translateY(-2px);
}
</style> 