<template>
  <div id="app" class="small-container">
    <h1>Todo List</h1>

    <todo-form @add:todo="addTodo" />
    <todo-list 
      :todos="todos" 
      @delete:todo="deleteTodo"
      @edit:todo="editTodo" 
    />

  </div>
</template>

<script>
import TodoList from './components/todos/TodoList.vue'
import TodoForm from './components/todos/TodoForm.vue'

export default {
  name: 'App',
  components: {
    TodoList,
    TodoForm
  },
  data() {
    return {
      todos: [
        {
          id: 1,
          name: "One"
        },
        {
          id: 2,
          name: "Two"
        },
        {
          id: 3,
          name: "Three"
        }
      ]
    }
  },
  methods: {
    addTodo(params) {
      const lastId  = this.todos.length > 0 ? this.todos[this.todos.length - 1].id : 0;
      const id      = lastId + 1
      const newTodo = { ...params, id }
      this.todos    = [...this.todos, newTodo]
    },
    deleteTodo(params) {
      this.todos = this.todos.filter(
        todo => todo.id != params
      )
    },
    editTodo(id, updatedTodo) {
      this.todos = this.todos.map(todo =>
        todo.id === id ? updatedTodo : todo
      )
    }
  }
}
</script>

<style>
  .small-container {
    max-width: 580px;
  }
</style>
