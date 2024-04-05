<template>

<div class="app">
  <h2 class="title">To-Do List</h2>
  <div class="to-do">
    <input class="input-text" :class="{red_is_active : todos.redActive}" v-model="todos.todo" type="text"  placeholder="type text">
    <button class="button-add" @click="addToDo(todos.id++)">add</button>
    <button class="button-delete-all" @click="deleteToDo">delete all</button>
    <p>список задач: {{ todos.todoList.length }}</p>
    <hr color="black">
    <div v-for="(element,i) in todos.todoList" :key="element.id">
      <p>
        <span class="todo-id">{{ i+1 + ") "}}</span>
        <span class="todo-text" 
        :class="{todo_text_isShow : element.isComplete}"
        @dblclick="removeItem(i)"
        >{{ element.text }}</span>
        <input type="checkbox" v-model="element.isComplete">
      </p>  
    </div>
  </div>
</div>

</template>

<script setup>
import {ref} from "vue"

const todos = ref({
  todo: '',
  todoList: [],
  isDone: false,
  id: 0,
  redActive: false,
});

const addToDo = () => {
  if (todos.value.todo.trim() !== ''){
    todos.value.redActive = false;
    todos.value.todoList.push({
      id: todos.value.id,
      text: todos.value.todo,
      isComplete: todos.value.isDone,
    });
    todos.value.todo = '';
  } else {
    todos.value.redActive = true;
    todos.value.todo = '';
    
  }
}
const deleteToDo = () => {
  todos.value.todoList = [];
  todos.value.id = 0;
}
const removeItem = (index) => {
  console.log(index);
  todos.value.todoList.splice(index,1)
}
</script>


<style scoped>
@import "./assets/global.css";
@import url('https://fonts.googleapis.com/css2?family=Lato:ital,wght@0,100;0,300;0,400;0,700;0,900;1,100;1,300;1,400;1,700;1,900&family=Ubuntu:ital,wght@0,300;0,400;0,500;0,700;1,300;1,400;1,500;1,700&display=swap');
.app{
  font-family: "Ubuntu", sans-serif;
  font-weight: 600;
  font-style: normal;
  width: 60%;
  margin: 0 auto;
  background-color: aqua;
  border-radius: 10px;
  padding: 10px 40px;
  min-height: 400px;
  outline: solid 3px #000;

}
.input-text{
  width:250px;
  height: 20px;

}
.red_is_active{
  border-color: red;
  transition: 0.5s;
  
}
.input-text:checked + span{
  text-decoration: line-through;
}
.button-add{
  height: 25px;
  background-color: #87CEFA;
  border: none;
  cursor: pointer;
}
.button-delete-all{
  height: 25px;
  background-color: #E9967A;
  border: none;
  cursor: pointer;
}
.todo_text_isShow{
  text-decoration: line-through;
  color: #808080;
}
</style>
