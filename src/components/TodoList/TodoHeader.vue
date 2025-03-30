<template>
  <header class="todo-header">
    <h1>Vue TodoList</h1>
    <a href="https://github.com/3268676707/vue-todolist" target="_blank" class="github-link">
      <i class="fab fa-github"></i> 查看源码
    </a>
  </header>
</template>

<script setup>
// 无需额外的逻辑
</script>

<style scoped>
.todo-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 20px;
  background-color: #f8f9fa;
  border-bottom: 1px solid #e9ecef;
  margin-bottom: 20px;
}

h1 {
  margin: 0;
  color: #2c3e50;
  font-size: 24px;
}

.github-link {
  display: flex;
  align-items: center;
  gap: 8px;
  color: #2c3e50;
  text-decoration: none;
  padding: 8px 16px;
  border-radius: 4px;
  background-color: #fff;
  border: 1px solid #e9ecef;
  transition: all 0.3s ease;
}

.github-link:hover {
  background-color: #f1f3f5;
  transform: translateY(-2px);
}
</style> 