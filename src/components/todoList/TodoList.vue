<template>
  <div class="todo-list">
    <TodoItem v-for="item in todolist" :key="item.id" :item="item" v-on="$listeners" />
  </div>
</template>

<script>
import TodoItem from "./TodoItem";
export default {
  name: "TodoList",
  props: ["todolist"],
  components: {
    TodoItem
  }
};
</script>

<style>
</style>