<template>
  <li class="todo-item" :class="{ completed: todo.completed }">
    <input 
      type="checkbox" 
      :checked="todo.completed"
      @change="$emit('update:todo', { ...todo, completed: $event.target.checked })"
      class="todo-checkbox"
    >
    <span class="todo-text">{{ todo.text }}</span>
    <button @click="$emit('delete')" class="delete-button">
      <i class="fas fa-trash"></i>
    </button>
  </li>
</template>

<script setup>
import { defineProps, defineEmits } from 'vue'

defineProps({
  todo: {
    type: Object,
    required: true
  }
})

defineEmits(['delete', 'update:todo'])
</script>

<style scoped>
.todo-item {
  display: flex;
  align-items: center;
  padding: 20px;
  margin-bottom: 12px;
  background: rgba(255, 255, 255, 0.8);
  border-radius: 12px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.05);
  transition: all 0.3s ease;
  border: 1px solid rgba(226, 232, 240, 0.8);
}

.todo-item:hover {
  transform: translateY(-2px);
  box-shadow: 0 6px 12px rgba(0, 0, 0, 0.1);
}

.todo-checkbox {
  width: 22px;
  height: 22px;
  margin-right: 20px;
  cursor: pointer;
  border-radius: 6px;
  border: 2px solid #4CAF50;
  position: relative;
  appearance: none;
  background: white;
  transition: all 0.3s ease;
}

.todo-checkbox:checked {
  background: #4CAF50;
}

.todo-checkbox:checked::after {
  content: '✓';
  position: absolute;
  color: white;
  font-size: 14px;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}

.todo-text {
  flex: 1;
  font-size: 16px;
  color: #2d3748;
  transition: all 0.3s ease;
}

.completed .todo-text {
  text-decoration: line-through;
  color: #a0aec0;
}

.delete-button {
  background: none;
  border: none;
  color: #ff4444;
  cursor: pointer;
  padding: 8px;
  border-radius: 8px;
  transition: all 0.3s ease;
  opacity: 0.7;
}

.delete-button:hover {
  background-color: #fff5f5;
  color: #e53e3e;
  opacity: 1;
}
</style> 