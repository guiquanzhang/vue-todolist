<template>
  <li class="todo-item" :class="{ completed: todo.completed }">
    <input 
      type="checkbox" 
      v-model="todo.completed"
      class="todo-checkbox"
    >
    <span class="todo-text">{{ todo.text }}</span>
    <button @click="$emit('delete')" class="delete-button">
      <i class="fas fa-trash"></i>
    </button>
  </li>
</template>

<script setup>
defineProps({
  todo: {
    type: Object,
    required: true
  }
})

defineEmits(['delete'])
</script>

<style scoped>
.todo-item {
  display: flex;
  align-items: center;
  padding: 16px;
  margin-bottom: 8px;
  background-color: #fff;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0,0,0,0.05);
  transition: all 0.3s ease;
}

.todo-item:hover {
  transform: translateY(-2px);
  box-shadow: 0 4px 8px rgba(0,0,0,0.1);
}

.todo-checkbox {
  width: 20px;
  height: 20px;
  margin-right: 16px;
  cursor: pointer;
}

.todo-text {
  flex: 1;
  font-size: 16px;
  color: #2c3e50;
}

.completed .todo-text {
  text-decoration: line-through;
  color: #888;
}

.delete-button {
  background: none;
  border: none;
  color: #ff4444;
  cursor: pointer;
  padding: 8px;
  border-radius: 4px;
  transition: all 0.3s ease;
}

.delete-button:hover {
  background-color: #ffebee;
  color: #d32f2f;
}
</style> 