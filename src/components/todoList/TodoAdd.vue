<template>
  <div class="input-add">
    <input type="text" v-model="myvalue" placeholder="Please input todo" @keydown="inputdone" />
    <button @click="addClick">
      <i class="add"></i>
    </button>
  </div>
</template>

<script>
export default {
  name: "TodoAdd",
  data() {
    return {
      myvalue: ""
    };
  },
  methods: {
    addClick() {
      this.$emit("handleClick", this.myvalue);
      this.myvalue = "";
    },
    inputdone(e) {
      if (e.code == "Enter") this.$emit("inputdone", this.myvalue);
      this.myvalue = "";
    }
  }
};
</script>

<style>
.input-add {
  position: relative;
  display: flex;
  align-items: center;
  margin: 0 20px;
  border-radius: 30px;
  box-shadow: 0 0 3px 2px rgba(0, 0, 0, 0.2);
}

.input-add input {
  width: 100%;
  padding: 10px 25px 10px 15px;
  border-radius: 30px;
  border: none;
  outline: none;
  font-size: 14px;
  color: #626262;
}

.input-add button {
  position: absolute;
  right: 0;
  width: 37px;
  height: 37px;
  border-radius: 50%;
  border: none;
  color: white;
  outline: none;
  background: #f9c3cc;
  cursor: pointer;
}

.input-add .add {
  display: block;
  margin: 5px;
  width: 37px;
  height: 37px;
  background: url("../../assets/images/add.png") no-repeat;
}
</style>