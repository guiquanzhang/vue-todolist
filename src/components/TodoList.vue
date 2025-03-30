<template>
  <div class="todo-container">
    <h1>我的待办事项</h1>
    
    <!-- 添加新任务 -->
    <div class="add-todo">
      <input 
        v-model="newTodo" 
        @keyup.enter="addTodo"
        placeholder="请输入新的待办事项"
        type="text"
      >
      <button @click="addTodo">添加</button>
    </div>

    <!-- 任务统计 -->
    <div class="todo-stats">
      <p>总任务数: {{ totalTodos }}</p>
      <p>已完成: {{ completedTodos }}</p>
      <p>未完成: {{ remainingTodos }}</p>
    </div>

    <!-- 任务列表 -->
    <ul class="todo-list">
      <li v-for="(todo, index) in filteredTodos" :key="index" class="todo-item">
        <input 
          type="checkbox" 
          v-model="todo.completed"
        >
        <span :class="{ completed: todo.completed }">{{ todo.text }}</span>
        <button @click="removeTodo(index)" class="delete-btn">删除</button>
      </li>
    </ul>

    <!-- 过滤选项 -->
    <div class="filter-options">
      <button 
        v-for="filter in filters" 
        :key="filter.value"
        @click="currentFilter = filter.value"
        :class="{ active: currentFilter === filter.value }"
      >
        {{ filter.label }}
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'TodoList',
  data() {
    return {
      todos: [],
      newTodo: '',
      currentFilter: 'all',
      filters: [
        { label: '全部', value: 'all' },
        { label: '待完成', value: 'active' },
        { label: '已完成', value: 'completed' }
      ]
    }
  },
  computed: {
    totalTodos() {
      return this.todos.length
    },
    completedTodos() {
      return this.todos.filter(todo => todo.completed).length
    },
    remainingTodos() {
      return this.todos.filter(todo => !todo.completed).length
    },
    filteredTodos() {
      switch (this.currentFilter) {
        case 'active':
          return this.todos.filter(todo => !todo.completed)
        case 'completed':
          return this.todos.filter(todo => todo.completed)
        default:
          return this.todos
      }
    }
  },
  methods: {
    addTodo() {
      if (this.newTodo.trim()) {
        this.todos.push({
          text: this.newTodo,
          completed: false
        })
        this.newTodo = ''
      }
    },
    removeTodo(index) {
      this.todos.splice(index, 1)
    }
  },
  created() {
    // 从localStorage加载数据
    const savedTodos = localStorage.getItem('todos')
    if (savedTodos) {
      this.todos = JSON.parse(savedTodos)
    }
  },
  watch: {
    todos: {
      handler(newTodos) {
        // 保存到localStorage
        localStorage.setItem('todos', JSON.stringify(newTodos))
      },
      deep: true
    }
  }
}
</script>

<style scoped>
.todo-container {
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
}

.add-todo {
  display: flex;
  gap: 10px;
  margin-bottom: 20px;
}

.add-todo input {
  flex: 1;
  padding: 8px;
  border: 1px solid #ddd;
  border-radius: 4px;
}

button {
  padding: 8px 16px;
  background-color: #4CAF50;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

button:hover {
  background-color: #45a049;
}

.todo-stats {
  margin-bottom: 20px;
  padding: 10px;
  background-color: #f5f5f5;
  border-radius: 4px;
}

.todo-list {
  list-style: none;
  padding: 0;
}

.todo-item {
  display: flex;
  align-items: center;
  padding: 10px;
  margin-bottom: 5px;
  background-color: #fff;
  border: 1px solid #ddd;
  border-radius: 4px;
}

.todo-item span {
  flex: 1;
  margin: 0 10px;
}

.completed {
  text-decoration: line-through;
  color: #888;
}

.delete-btn {
  background-color: #f44336;
}

.delete-btn:hover {
  background-color: #da190b;
}

.filter-options {
  margin-top: 20px;
  display: flex;
  gap: 10px;
}

.filter-options button {
  background-color: #f5f5f5;
  color: #333;
}

.filter-options button.active {
  background-color: #4CAF50;
  color: white;
}
</style> 