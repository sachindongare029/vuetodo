<template>
  <div class="todo__input" id="input_container">
    <input
      class="form-control"
      type="text"
      placeholder="Create a new to-do..."
      v-on:keyup.enter="inputChanged"
    />
  </div>
</template>

<script>
import { EventBus } from "./EventBus.js";
export default {
  name: "TodoInput",
  data: function () {
    return {
      todos: [],
    };
  },
  mounted() {
    EventBus.$on("todo-deleted", todo => {
      var updated = this.todos.filter((el) => {
        return el.id !== todo.id;
      });
      this.todos = updated;
    });
  },
  methods: {
    inputChanged: function (e) {
      if (!e.target.value) return;
      this.todos.push({
        id: Math.random().toString(36).substr(2, 9),
        todo: e.target.value,
      });
      EventBus.$emit("todo-added", this.todos);
      e.target.value = "";
    },
  },
};
</script>

<style scoped>
input {
  width: 60%;
  padding: 8px;
  border: 1px solid #525252;
}
</style>
