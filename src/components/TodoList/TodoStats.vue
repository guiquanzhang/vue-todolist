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
  padding: 20px;
  background-color: #f8f9fa;
  border-radius: 8px;
  margin-bottom: 20px;
  box-shadow: 0 2px 4px rgba(0,0,0,0.05);
}

.stat-item {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 8px;
}

.stat-label {
  color: #6c757d;
  font-size: 14px;
}

.stat-value {
  font-size: 24px;
  font-weight: bold;
  color: #2c3e50;
}

.completed {
  color: #4CAF50;
}

.remaining {
  color: #ff9800;
}
</style> 