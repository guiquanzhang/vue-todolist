<template>
  <div class="todo-filter">
    <button 
      v-for="filter in filters" 
      :key="filter.value"
      @click="$emit('update:modelValue', filter.value)"
      :class="{ active: modelValue === filter.value }"
      class="filter-button"
    >
      {{ filter.label }}
    </button>
  </div>
</template>

<script setup>
import { defineProps, defineEmits } from 'vue'

defineProps({
  modelValue: {
    type: String,
    required: true
  }
})

defineEmits(['update:modelValue'])

const filters = [
  { label: '全部', value: 'all' },
  { label: '待完成', value: 'active' },
  { label: '已完成', value: 'completed' }
]
</script>

<style scoped>
.todo-filter {
  display: flex;
  gap: 10px;
  margin-top: 20px;
  justify-content: center;
}

.filter-button {
  padding: 8px 16px;
  background-color: #f8f9fa;
  color: #6c757d;
  border: 1px solid #e9ecef;
  border-radius: 6px;
  cursor: pointer;
  transition: all 0.3s ease;
}

.filter-button:hover {
  background-color: #e9ecef;
  transform: translateY(-2px);
}

.filter-button.active {
  background-color: #4CAF50;
  color: white;
  border-color: #4CAF50;
}
</style> 