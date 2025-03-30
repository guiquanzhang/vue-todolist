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
import { ref, defineEmits } from 'vue'

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
  gap: 15px;
  margin-bottom: 25px;
}

.todo-input-field {
  flex: 1;
  padding: 15px 20px;
  border: 2px solid #e2e8f0;
  border-radius: 12px;
  font-size: 16px;
  transition: all 0.3s ease;
  background: rgba(255, 255, 255, 0.8);
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.05);
}

.todo-input-field:focus {
  outline: none;
  border-color: #4CAF50;
  box-shadow: 0 0 0 3px rgba(76, 175, 80, 0.2);
}

.add-button {
  padding: 15px 30px;
  background: linear-gradient(45deg, #4CAF50, #45a049);
  color: white;
  border: none;
  border-radius: 12px;
  cursor: pointer;
  font-size: 16px;
  font-weight: 500;
  display: flex;
  align-items: center;
  gap: 8px;
  transition: all 0.3s ease;
  box-shadow: 0 4px 15px rgba(76, 175, 80, 0.2);
}

.add-button:hover {
  transform: translateY(-2px);
  box-shadow: 0 6px 20px rgba(76, 175, 80, 0.3);
}

.add-button:active {
  transform: translateY(0);
}
</style> 