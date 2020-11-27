<template>
  <div id="app" class="todo__container container">
    <TodoHeader />
    <TodoInput />
    <Todos />
  </div>
</template>

<script>
import TodoHeader from "./components/TodoHeader.vue";
import TodoInput from "./components/TodoInput.vue";
import Todos from "./components/Todos.vue";

export default {
  name: "App",
  components: {
    TodoHeader,
    TodoInput,
    Todos,
  },
};
</script>

<style>
body {
  height: 100vh;
  background: #a9a9a9 !important;
}
.todo__container {
  margin-top: 20px;
}
</style>
