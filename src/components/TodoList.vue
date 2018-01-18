<template>
<div>
  <ul v-for="(todo, index) in todos" v-bind:key="index">
    <li>
      <template v-if="todo.completed">
        <s>{{ todo.text }}</s>
      </template>
      <template v-else>
        {{ todo.text }}
      </template>
      <template v-if="todo.completed">
        <button v-on:click="toggleStatus(todo.id)">Uncomplete</button>
      </template>
      <template v-else>
        <button v-on:click="toggleStatus(todo.id)">Complete</button>
      </template>
      <button v-on:click="remove(todo.id)">X</button>
    </li>
  </ul>
</div>
</template>

<script>
export default {
  name: 'TodoList',
  props: {
    todos: {
      type: Array,
      Required: true
    }
  },
  methods: {
    remove: function (index) {
      this.$emit('remove', index)
    },
    toggleStatus: function (index) {
      this.$emit('toggleStatus', index)
    }
  }
}
</script>

<style>

</style>
