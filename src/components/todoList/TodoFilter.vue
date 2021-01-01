<template>
  <div class="todo-filter">
    <span
      v-for="f in filters"
      :key="f.value"
      :class="{active: f.value === selected}"
      @click="$emit('changefilter',f.value);"
    >{{f.label}}</span>
    <button @click="$emit('cleardone')">清除已完成</button>
  </div>
</template>

<script>
export default {
  name: "TodoFilter",
  props: ["selected"],
  data() {
    return {
      filters: [
        { label: "全部", value: "all" },
        { label: "已完成", value: "done" },
        { label: "未完成", value: "todo" }
      ],
      active: "active"
    };
  },
  methods: {
    changefilter() {}
  }
};
</script>

<style>
.todo-filter {
  position: relative;
  margin: 12px 20px;
  color: rgb(180, 178, 178);
}

.todo-filter span {
  transition: ease 0.7;
  margin: 0 10px;
  font-size: 14px;
  cursor: pointer;
}

.todo-filter .active {
  color: rgb(80, 74, 74);
  font-size: 15px;
}

.todo-filter button {
  position: absolute;
  right: 0;
  padding: 2px 10px;
  background-color: #fff;
  border: 1px solid #ccc;
  border-radius: 10px;
  outline: none;
  cursor: pointer;
  color: rgb(134, 129, 129);
}
</style>