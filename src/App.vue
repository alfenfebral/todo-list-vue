<template>
  <div id="app">
    <h1> Todos Vue</h1>
    <form v-on:submit.prevent="todoSubmit">
      <input type="text" name="name" v-model="name">
      <input type="submit" value="Submit">
    </form>
    <br>
    <button v-on:click="statusAll">All</button>
    <button v-on:click="statusCompleted">Completed</button>
    <button v-on:click="statusNotCompleted">Not Completed</button>
    <TodoList v-bind:todos="todoFilter"
     v-on:remove="remove($event)"
     v-on:toggleStatus="toggleStatus($event)"/>    
  </div>
</template>

<script>
import TodoList from './components/TodoList'

export default {
  name: 'app',
  components: {
    TodoList
  },
  data () {
    return {
      name: '',
      todos: [
        { id: 1, text: 'Learn JavaScript', completed: true },
        { id: 2, text: 'Learn Vue', completed: false },
        { id: 3, text: 'Build something awesome', completed: false }
      ],
      nextId: 4,
      filter: 'all'
    }
  },
  methods: {
    remove: function (index) {
      function getSameId (todo) {
        return todo.id === index
      }
      console.log('data removed id: ' + index + ' index: ' + this.todos.findIndex(getSameId))
      var indexId = this.todos.findIndex(getSameId)
      this.todos.splice(indexId, 1)
    },
    toggleStatus: function (index) {
      function getSameId (todo) {
        return todo.id === index
      }
      console.log('toggle status id: ' + index + ' index: ' + this.todos.findIndex(getSameId))

      var indexId = this.todos.findIndex(getSameId)
      this.todos.splice(this.todos.findIndex(getSameId), 1, {
        id: this.todos[indexId].id,
        text: this.todos[indexId].text,
        completed: !this.todos[indexId].completed
      })
    },
    todoSubmit: function () {
      this.todos.push({
        id: this.nextId++,
        text: this.name,
        completed: false
      })
      this.name = ''
    },
    statusCompleted: function () {
      this.filter = 'completed'
    },
    statusNotCompleted: function () {
      this.filter = 'not completed'
    },
    statusAll: function () {
      this.filter = 'all'
    }
  },
  computed: {
    todoFilter: function () {
      if (this.filter === 'all') {
        return this.todos
      } else {
        var completed = (this.filter === 'completed')
        return this.todos.filter(todo => {
          return todo.completed === completed
        })
      }
    }
  }
}
</script>

<style>

</style>
