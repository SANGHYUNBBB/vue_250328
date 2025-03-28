<script>
import HeaderLayout from './components/HeaderLayout.vue'
import InputContainer from './components/InputContainer.vue'
import FilterContainer from './components/FilterContainer.vue'
import TodoItem from './components/TodoItem.vue'
import SummaryContainer from './components/SummaryContainer.vue'
export default {
  name: 'App',
  data() {
    return {
      todos: [
        {
          id: 1,
          text: '할 일 1',
          completed: false,
          createAt: '2025-03-24',
        },
        {
          id: 2,
          text: '할 일 2',
          completed: true,
          createAt: '2025-03-25',
        },
        {
          id: 3,
          text: '할 일 3',
          completed: false,
          createAt: '2025-03-26',
        },
        {
          id: 4,
          text: '할 일 4',
          completed: false,
          createAt: '2025-03-26',
        },
      ],
      filter: 'all',
    }
  },
  components: {
    SummaryContainer,
    TodoItem,
    InputContainer,
    HeaderLayout,
    FilterContainer,
  },
  methods: {
    addTodo(newtodo) {
      const text = this.newTodo
      if (!text)
        return this.todos.push({
          id: Date.now(),
          text: newtodo,
          completed: false,
          createAt: new Date().toLocaleDateString(),
        })
    },
    toggleCompleted(id) {
      const todo = this.todos.find((todo) => todo.id === id)
      todo.completed = !todo.completed
    },
    removeTodo(id) {
      this.todos = this.todos.filter((todo) => todo.id !== id)
    },
    saveTodos() {
      const todos = localStorage.setItem('todos')
      todos ? (this.todos = JSPN.parse(todos)) : []
    },
    loadTodos() {
      const todos = localStorage.getItem('todos')
      todos ? (this.todos = JSPN.parse(todos)) : []
    },
    clearCompleted() {
      this.todos = this.todos.filter((todo) => todo.completed).length
      this.saveTodos()
    },
    filterChange(filter) {
      this.filter = filter
    },
  },
  computed: {
    // filteredTodos() {
    //   if (this.filter === 'active') {
    //     return this.todos.filter((todo) =>)
    //   }
    // },
    activeTodoCount() {
      return this.todos.filter((todo) => !todo.completed).length
    },
    completedTodoCount() {
      return this.todos.filter((todo) => todo.completed).length
    },
  },
}
</script>

<template>
  <div class="app"></div>
  <HeaderLayout title="작심" />
  <InputContainer @add-todo="addTodo" />
  <FilterContainer @filter-changed="filterChanged" />
  <ul class="todo-list">
    <TodoItem
      v-for="todo in todos"
      :key="todo.id"
      :todo="todo"
      @toggle-completed="toggleCompleted"
    />
  </ul>
  <SummaryContainer :activeTodoCount="activeTodoCount" :completedTodoCount="completedTodoCount" />
</template>

<style scoped>
.todo-list {
  margin: var(--space-l) auto !important;
}
</style>
