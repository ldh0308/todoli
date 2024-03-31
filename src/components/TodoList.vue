<template>
  <div>
    <ul>
      <li v-for="(todoItem, index) in todoItems" v-bind:key="todoItem" class="shadow">
        {{ todoItem }}
      <span class="removeBtn" v-on:click="removeTodo(todoItem, index)"> <!--methods에 todoItem,index를 넘길 수 있다)-->
        <i class="fa-solid fa-trash"></i> <!--font awesome에서 가져온 아이콘-->
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
    removeTodo: function(todoItem, index) {
        console.log(todoItem, index+1);
        localStorage.removeItem(todoItem); //로컬만 delete
        this.todoItems.splice(index, 1); // 화면단도 delete
    }
  },
  // 인스턴스가 생성되면서 불러와지는 로직 created
  created: function () {
    if (localStorage.length > 0) {
      for (var i = 0; i < localStorage.length; i++) {
        this.todoItems.push(localStorage.key(i));
        // test
        // console.log(localStorage.key(i))
      }
    }
  },
};
</script>

<style>
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
</style>