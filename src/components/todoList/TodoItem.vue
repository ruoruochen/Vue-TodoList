<template>
  <div class="todo-item">
    <input type="checkbox" class="todo-check" @change="checkchange" :checked="isChecked" />
    <span class="todo-text">{{item.text}}</span>
    <input type="text" value class="input-text" @keydown="changetext" />
    <i class="edit" @click="editItem"></i>
    <i class="delete" @click="deleteItem"></i>
  </div>
</template>

<script>
export default {
  name: "TodoItem",
  props: ["item"],
  data() {
    return {
      isChecked: this.item.state == "done"
    };
  },
  methods: {
    deleteItem() {
      this.$emit("deleteitem", this.item.id);
    },
    editItem() {
      this.$emit("edititem", this.item.id);
    },
    changetext(e) {
      if (e.code == "Enter") this.$emit("changetext", this.item.id);
    },
    checkchange() {
      this.$emit("checkchange", this.item.id);
    }
  }
};
</script>

<style>
.todo-item {
  position: relative;
  display: flex;
  align-items: center;
  justify-items: center;
  background-color: #fff;
  margin: 8px 20px;
  padding: 10px;
  border-radius: 20px;
}

.todo-item .todo-check:checked + .todo-text {
  text-decoration: line-through;
  color: #c0bdbd;
  transition: 0.1s;
}

.todo-check {
  position: absolute;
  left: 10px;
  width: 16px;
  height: 16px;
  border-radius: 50%;
}

.todo-item .todo-text {
  transition: 0.1s;
  display: block;
  overflow-wrap: break-word;
  width: 78%;
  margin: 0 10px 0 20px;
  padding: 5px 10px;
  border: none;
  font-size: 16px;
}

.todo-item .input-text {
  position: absolute;
  left: 40px;
  font-size: 16px;
  border: none;
  outline: none;
  display: none;
}

.todo-item .edit {
  position: absolute;
  right: 30px;
  display: block;
  width: 28px;
  height: 28px;
  margin-right: 5px;
  background: url("../../assets/images/edit.png") no-repeat;
  background-size: 20px;
  cursor: pointer;
}
.todo-item .delete {
  position: absolute;
  right: 1px;
  display: block;
  width: 28px;
  height: 28px;
  margin-right: 5px;
  background: url("../../assets/images/delete.png") no-repeat;
  background-size: 20px;
  cursor: pointer;
}
</style>