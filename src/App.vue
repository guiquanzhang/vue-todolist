<template>
  <div id="app">
    <TodoList />
  </div>
</template>

<script setup>
import TodoList from './components/TodoList/index.vue'
</script>

<style>
@import url('https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.4/css/all.min.css');

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  background-color: #f5f5f5;
  color: #2c3e50;
}

#app {
  min-height: 100vh;
  padding: 20px;
}
</style> 