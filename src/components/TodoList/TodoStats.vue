<template>
  <div class="todo-stats">
    <div class="stat-item">
      <span class="stat-label">总任务数</span>
      <span class="stat-value">{{ total }}</span>
    </div>
    <div class="stat-item">
      <span class="stat-label">已完成</span>
      <span class="stat-value completed">{{ completed }}</span>
    </div>
    <div class="stat-item">
      <span class="stat-label">未完成</span>
      <span class="stat-value remaining">{{ remaining }}</span>
    </div>
  </div>
</template>

<script setup>
import { defineProps } from 'vue'

defineProps({
  total: {
    type: Number,
    required: true
  },
  completed: {
    type: Number,
    required: true
  },
  remaining: {
    type: Number,
    required: true
  }
})
</script>

<style scoped>
.todo-stats {
  display: flex;
  justify-content: space-between;
  padding: 25px;
  background: rgba(255, 255, 255, 0.9);
  border-radius: 16px;
  margin-bottom: 25px;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.05);
  backdrop-filter: blur(5px);
  border: 1px solid rgba(255, 255, 255, 0.3);
}

.stat-item {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 10px;
  padding: 0 20px;
  position: relative;
}

.stat-item:not(:last-child)::after {
  content: '';
  position: absolute;
  right: 0;
  top: 50%;
  transform: translateY(-50%);
  height: 70%;
  width: 1px;
  background: rgba(0, 0, 0, 0.1);
}

.stat-label {
  color: #64748b;
  font-size: 14px;
  font-weight: 500;
  text-transform: uppercase;
  letter-spacing: 0.5px;
}

.stat-value {
  font-size: 28px;
  font-weight: 600;
  color: #1a365d;
}

.completed {
  color: #4CAF50;
}

.remaining {
  color: #f59e0b;
}
</style> 