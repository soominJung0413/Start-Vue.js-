<template lang="html">
  <div id="app">
    <TodoHeader></TodoHeader>
    <TodoInput v-on:addTodo="addTodo"></TodoInput>
    <TodoList v-bind:propsdata="todoItems" @removeTodo="removeTodo"></TodoList>
    <TodoFooter v-on:removeAll="clearAll"></TodoFooter>
  </div>
</template>

<script>
import TodoHeader from './components/TodoHeader.vue'// ES6 에서 추가된 import - from 구문 import 담을그릇 from 파일경로77777777777
import TodoInput from './components/TodoInput.vue'
import TodoList from './components/TodoList.vue'
import TodoFooter from './components/TodoFooter.vue'

export default {
  components : {
    'TodoHeader' : TodoHeader,
    'TodoInput' : TodoInput,
    'TodoList' : TodoList,
    'TodoFooter' : TodoFooter
  },
    created() {
        if(localStorage.length > 0){
            for(let i = 0; i<localStorage.length; i++){
                this.todoItems.push(localStorage.key(i));
            }
        }
    },
    data() {
      return {
          todoItems: []
      }
    },
    methods : {
      addTodo(TodoItem){// 이벤트에서 넘어온 데이터
        localStorage.setItem(TodoItem,TodoItem);//로컬스토리지 저장
        this.todoItems.push(TodoItem);// 상위 컴포넌트의 데이터 속성에 저장.
      },
      clearAll(){
          localStorage.clear();
          this.todoItems = [];
      },
      removeTodo(todoItem, index){
        localStorage.removeItem(todoItem);
        this.todoItems.splice(index,1);
      }
    }

}
</script>

<style lang="css">
  body {
    text-align: center;
    background-color: #F6F6F8;
  }
  input {
    border-style: groove;
    width: 200px;
  }
  button {
    border-style: groove;
  }
  .shadow {
    box-shadow: 5px 10px 10px rgba(0,0,0,0.03);
  }
</style>
