<template>
  <div>
    <ul>
      <li
        v-for="(todoItem, index) in todoItems"
        v-bind:key="todoItem.item"
        class="shadow"
      >
        <i
          class="checkBtn fa-solid fa-check"
          v-bind:class="{ checkBtnCompleted: todoItem.completed }"
          v-on:click="toggleComplete(todoItem, index)"></i>
        <!-- completed 속성에 따라 동적으로 바뀜 true면 textCompleted, false면 todoItem.completed-->
        <span v-bind:class="{ textCompleted: todoItem.completed }">{{
          todoItem.item
        }}</span>
        <span class="removeBtn" v-on:click="removeTodo(todoItem, index)">
          <!--methods에 todoItem,index를 넘길 수 있다)-->
          <i class="fa-solid fa-trash"></i>
          <!--font awesome에서 가져온 아이콘-->
        </span>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data: function () {
    return {
      todoItems: [],
    };
  },
  methods: {
    removeTodo: function (todoItem, index) {
      console.log(todoItem, index + 1);
      localStorage.removeItem(todoItem); //로컬만 delete
      this.todoItems.splice(index, 1); // 화면단도 delete
    },
    toggleComplete: function (todoItem) {
        // complete toggle 로직
        todoItem.completed = !todoItem.completed;
        // 로컬 스토리지 데이터 갱신
        localStorage.removeItem(todoItem.item);
        localStorage.setItem(todoItem.item, JSON.stringify(todoItem));
    },
  },
  // 인스턴스가 생성되면서 불러와지는 로직 created
  created: function () {
    if (localStorage.length > 0) {
      for (var i = 0; i < localStorage.length; i++) {
        this.todoItems.push(
          JSON.parse(localStorage.getItem(localStorage.key(i)))
        );
        // test
        // console.log(localStorage.key(i))
      }
    }
  },
};
</script>

<style scoped>
ul {
  list-style-type: none; /*점없애는 스타일링*/
  padding-left: 0px;
  margin-top: 0;
  text-align: left;
}
li {
  display: flex;
  min-height: 50px;
  height: 50px;
  line-height: 50px;
  margin: 0.5rem 0;
  padding: 0 0.9rem;
  background: white;
  border-radius: 5px;
}
.checkBtn {
  line-height: 45px;
  color: #62acde;
  margin-right: 5px;
}
.checkBtnCompleted {
  color: #b3adad;
}
.removeBtn {
  margin-left: auto;
  color: #de4343;
}
.textCompleted {
  text-decoration: line-through;
  color: #b3adad;
}
</style>