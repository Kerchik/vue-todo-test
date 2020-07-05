<template>
  <div>
    <h2>Todo application</h2>
    <router-link to="/">Home</router-link>
    <hr>
    <AddTodo @add-todo="addTodo" />
    <select v-model="filter">
      <option value="all">All</option>
      <option value="completed">Completed</option>
      <option value="not-completed">Not completed</option>
    </select>
    <Loader v-if="loading"/>
    <TodoList
      v-else-if="todos.length" 
      v-bind:todos="filteredTodos"
      @remove-todo="removeTodo"
    />
    <p v-else>No elements</p>
  </div>
</template>

<script>

import TodoList from '@/components/TodoList'
import AddTodo from '@/components/AddTodoComponent'
import Loader from '@/components/Loader'
export default {
  name: 'App',
  data() {
    return {
      todos: [],
      loading: true,
      filter: 'all'
    }
  },
  components: {
    TodoList,
    AddTodo,
    Loader
  },
  mounted() {
    fetch('https://jsonplaceholder.typicode.com/todos?_limit=3')
      .then(response => response.json())
      .then(json => {
        this.todos = json
        this.loading = false
      })
  },
  computed: {
    filteredTodos() {
      if (this.filter === 'all') {
        return this.todos
      } 
      if (this.filter === 'completed') {
        return this.todos.filter(t => t.completed === true)
      }
      if (this.filter === 'not-completed') {
        return this.todos.filter(t => t.completed === false)
      }

    }
  },
  methods: {
    removeTodo(id) {
      this.todos = this.todos.filter(todo => {
         return todo.id !== id
      })
    },
    addTodo(newTodo) {
      console.log(newTodo)
      this.todos.push(newTodo)
    }
  }
}
</script>