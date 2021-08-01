<template>
  <h1>Vue 3 Demo</h1>
  <form @submit.prevent="addTodo">
    <label>New Todo</label>
    <input v-model="newTodo" name="newTodo">
    <button>Add New Todo</button>
  </form>
  <button @click="allDone">All Done</button>
  <button @click="clearTodo">Clear Todo</button>
  <ul>
    <li v-for="(todo, index) in todos" :key="todo.id" class="todo">
      <h3 :class="{ done: todo.done }" @click="toggleDone(todo)">{{todo.content}}</h3>
      <button @click="deleteTodo(index)">Delete Todo</button>
    </li>
  </ul>
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const newTodo = ref('');
    const todos = ref([]);

    function addTodo() {
      todos.value.push(
          {
            id: Date.now(),
            content: newTodo.value,
            done: false,
          }
      );
      newTodo.value = '';
    }

    function toggleDone(todo) {
      todo.done = !todo.done;
    }

    function deleteTodo(index) {
      todos.value.splice(index, 1);
    }

    function allDone() {
      todos.value.forEach((todo) => todo.done = true);
    }

    function clearTodo() {
      todos.value = [];
    }

    return {
      clearTodo,
      allDone,
      deleteTodo,
      toggleDone,
      todos,
      newTodo,
      addTodo,
    };
  }
}
</script>

<style>
  body {
    font-family: sans-serif;
    padding-top: 1em;
    padding-bottom: 1em;
    font-size: 2em;
    width: 80%;
    margin: 0 auto;
  }
  input, textarea, button, p, div, section, article, select {
    display: block;
    width: 100%;
    font-family: sans-serif;
    font-size: 1em;
    margin: 0.5em;
  }

  .done {
    text-decoration: line-through;
  }

  .todo {
    cursor: pointer;
  }
</style>
