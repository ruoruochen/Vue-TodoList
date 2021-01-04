<template>
  <main>
    <div id="app" class="container">
      <h1 class="title">TodoList</h1>
      <TodoAdd @handleClick="handleClick" @inputdone="inputdone" />
      <TodoFilter :selected="selected" @changefilter="changefilter" @cleardone="cleardone" />
      <TodoList
        :todolist="todolistFilter"
        @deleteitem="deleteItem"
        @edititem="editItem"
        @changetext="changetext"
        @checkchange="checkchange"
      />
    </div>
  </main>
</template>

<script>
import TodoAdd from "../components/todoList/TodoAdd";
import TodoFilter from "../components/todoList/TodoFilter";
import TodoList from "../components/todoList/TodoList";
export default {
  name: "app",
  data() {
    return {
      todolist: [],
      selected: "all"
    };
  },
  methods: {
    //点击添加按钮
    // 获取本地存储数据
    // 将任务存入本地存储
    // 保存数据
    // 赋值给todolist
    handleClick(v) {
      if (v == "") {
        alert("Todo项不能为空！");
        return;
      }
      let data = this.getData();
      let id = data.length + 1;
      data.push({ id: id, text: v, state: "todo" });
      this.saveData(data);
      this.todolist = data;
      this.inputValue = "";
      this.id++;
    },
    //回车为Enter自动提交
    inputdone(v) {
      this.handleClick(v);
    },
    //筛选状态
    changefilter(s) {
      console.log(s);
      this.selected = s;
    },
    //编辑Todo 显示input框
    editItem(id) {
      console.log("editItem");
      var index = this.todolist.findIndex(item => item.id === id);
      var inputText = document.querySelectorAll(".input-text");
      inputText[index].style.display = "block";
      inputText[index].value = this.todolist[index].text;
      inputText[index].focus();
    },
    //编辑Todo 回车时修改数据并隐藏Input框
    changetext(id) {
      console.log("changetext" + id);
      var index = this.todolist.findIndex(item => item.id === id);
      var inputText = document.querySelectorAll(".input-text");
      if (inputText[index].value == "") alert("不能为空!");
      inputText[index].style.display = "none";
      this.todolist[index].text = inputText[index].value;
      this.saveData(this.todolist);
    },
    //删除Todo
    deleteItem(id) {
      this.todolist.splice(
        this.todolist.findIndex(item => item.id === id),
        1
      );
      this.saveData(this.todolist);
    },
    //改变check状态 修改数据
    checkchange(id) {
      console.log("checkchange" + id);
      var index = this.todolist.findIndex(item => item.id === id);
      var checks = document.querySelectorAll(".todo-check");
      if (checks[index].checked == true) this.todolist[index].state = "done";
      else this.todolist[index].state = "todo";
      this.saveData(this.todolist);
    },
    //清除已完成Todo
    cleardone() {
      console.log("cleardone");
      this.todolist = this.todolist.filter(item => item.state === "todo");
      this.saveData(this.todolist);
    },
    //保存本地数据
    saveData(data) {
      localStorage.setItem("todolist", JSON.stringify(data));
    },
    //获取本地数据
    getData() {
      let data = localStorage.getItem("todolist");
      if (data != null) {
        return JSON.parse(data);
      } else {
        return [];
      }
    }
  },
  computed: {
    //数据筛选
    todolistFilter() {
      return this.todolist.filter(v => {
        if (this.selected == "all") return true;
        else return v.state == this.selected;
      });
    }
  },
  components: {
    TodoAdd,
    TodoFilter,
    TodoList
  },
  created() {
    this.todolist = this.getData();
  }
};
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

main {
  width: 100%;
  min-height: 580px;
  display: flex;
  align-items: center;
  justify-content: center;
  background: url("../assets/images/bg.jpg") repeat-y 0 0;
  background-size: 100%;
}

.container {
  width: 40%;
  min-width: 400px;
  border-radius: 25px;
  box-shadow: 0px 0px 3px 3px rgba(0, 0, 0, 0.2);
  background-color: rgba(255, 255, 255, 0.7);
}
/* 239 110 130 */
.title {
  text-align: center;
  margin: 18px 0;
  font-size: 35px;
  color: rgba(239, 110, 130, 0.4);
}
</style>