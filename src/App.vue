<template>
  <h1>Todo app</h1>
  <form @submit.prevent="submitTodo">
    <label for="newTodo">New todo</label>
    <input
      type="text"
      name="newTodo"
      placeholder="type new todo here"
      v-model="newTodo"
    />
    <button>Add new todo</button>
  </form>
  <button @click="markAllDone">Mark all as done</button>
  <button @click="removeAllTodo">Remove all todo</button>
  <ul>
    <li
      v-for="(todo, index) in todos"
      :key="todo.id"
      class="todo"
      @click="toggleTodo(todo)"
    >
      <h3 :class="{ done: todo.done }">{{ todo.content }}</h3>
      <button @click="removeTodo(index)">Remove this</button>
    </li>
  </ul>
</template>

<script>
import { ref } from "vue";
export default {
  setup() {
    const newTodo = ref("");
    const todos = ref([]);
    function submitTodo() {
      todos.value.push({ id: Date.now(), done: false, content: newTodo.value });
      newTodo.value = "";
    }
    function toggleTodo(todo) {
      todo.done = !todo.done;
    }
    function removeTodo(index) {
      todos.value.splice(index, 1);
    }
    function markAllDone() {
      todos.value.forEach((todo) => (todo.done = true));
    }
    function removeAllTodo() {
      todos.value = [];
    }
    return {
      newTodo,
      todos,
      submitTodo,
      toggleTodo,
      removeTodo,
      markAllDone,
      removeAllTodo,
    };
  },
};
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
input,
textarea,
button,
p,
div,
section,
article,
select {
  display: "block";
  width: 100%;
  font-family: sans-serif;
  font-size: 1em;
  margin: 0.5em;
}
.todo {
  cursor: pointer;
}
.done {
  text-decoration: line-through;
}
.todo {
  cursor: "pointer";
}
</style>
