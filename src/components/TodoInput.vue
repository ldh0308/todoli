<template>
  <div class="inputBox shadow">
    <!-- input에 입력된 text 값을 바로바로 인스턴스 안에 mapping하는 역할 -->
    <input type="text" v-model="newTodoItem" v-on:keyup.enter="addTodo" />
    <!-- <button v-on:click="addTodo">add</button> -->
    <span class="addContainer" v-on:click="addTodo">
      <i class="fa-solid fa-plus addbtn"></i>
    </span>
  </div>
</template>

<script>
export default {
  data: function () {
    return {
      newTodoItem: "",
    };
  },
  methods: {
    addTodo: function () {
        // newTodoItem이 공백이 아닐때 
      if (this.newTodoItem !== "") {
        // completed 텍스트가 체크되었는지 안되었는지 boolean값 삽입
        // boolean값을 넣어서 스토리지 값에 넣을 예정
        var obj = { completed: false, item: this.newTodoItem };
        //자바스크립트 객체(obj)를 string값으로 넣어 주는 API
        localStorage.setItem(this.newTodoItem, JSON.stringify(obj));
        this.clearInput();
      }
    },
    clearInput: function () {
      this.newTodoItem = "";
    },
  },
};
</script>

<style scoped>
input:focus {
  outline: none;
}
.inputBox {
  background: white;
  height: 50px;
  line-height: 50px;
  border-radius: 5px;
}
.inputBox input {
  border-style: none;
  font-size: 0.9rem;
}
.addContainer {
  float: right;
  background: linear-gradient(to right, #6478fb, #8763fb);
  display: block;
  width: 3rem;
  border-radius: 0 5px 5px 0;
}
.addBtn {
  color: white;
  vertical-align: middle;
}
</style>