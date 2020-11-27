<template>
  <ul class="todos__container">
    <li class="todo__item" v-for="item in todos" :key="item.id">
      <button class="todo__title btn border-0">{{ item.todo }}</button>
      <button class="btn btn-outline-primary border-0">
        <font-awesome-icon :icon="['fa', 'edit']" />
      </button>
      <button
        class="todo__remove btn btn-outline-danger border-0"
        v-on:click="removeTodo(item)"
      >
        <font-awesome-icon :icon="['fa', 'trash']" />
      </button>
    </li>
  </ul>
</template>

<script>
import Vue from "vue";
import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";
import { library } from "@fortawesome/fontawesome-svg-core";
import { faTrash, faEdit } from "@fortawesome/free-solid-svg-icons";
import { EventBus } from "./EventBus.js";

library.add(faTrash, faEdit);
Vue.component("font-awesome-icon", FontAwesomeIcon);

export default {
  name: "Todos",
  data: function () {
    return {
      todos: [],
    };
  },
  mounted() {
    EventBus.$on("todo-added", todos => {
      this.todos = todos;
    });
  },
  methods: {
    removeTodo: function (todo) {
      var updated = this.todos.filter((el) => {
        return el.id !== todo.id;
      });
      this.todos = updated;
      EventBus.$emit("todo-deleted", todo);
    },
  },
};
</script>

<style scoped>
.todos__container {
  width: 50%;
  padding: 0;
  margin: 30px 0;
}
.todo__item {
  list-style: none;
  border: 1px solid #8a8a8a;
  border-bottom: none;
  background: #efefef;
  padding: 0.75rem 1.25rem;
  display: flex;
  justify-content: space-between;
}
.todo__item:first-child {
  border-top-left-radius: 7px;
  border-top-right-radius: 7px;
}
.todo__item:last-child {
  border-bottom: 1px solid #8a8a8a;
  border-bottom-left-radius: 7px;
  border-bottom-right-radius: 7px;
}
.todo__title {
  width: 90%;
  text-align: left;
  outline: none;
}
.btn.focus,
.btn:focus {
  box-shadow: none;
}
</style>