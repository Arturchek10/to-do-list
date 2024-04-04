<template>

<div class="app">
  <h2 class="title">To-Do List</h2>
  <div class="to-do">
    <p>{{ todo }}</p>
    <input class="input-text" v-model="todo" type="text"  placeholder="type text">
    <button class="button-add" @click="addToDo(id++)">add</button>
    <button class="button-delete-all" @click="deleteToDo">delete all</button>
    <div v-for="(element, index) in todoList" :key="index">
      <p>
        <span class="todo-id">{{ ++index + ") "}}</span>
        <span class="todo-text" :class="{todo_text_isShow : isDone}">{{ element }}</span>
        <input type="checkbox" v-model="isDone">
      </p>  
    </div>
  </div>
</div>

</template>

<script setup>
import {ref} from "vue"

const todo = ref('');
const todoList = ref([]);
const isDone = ref(false);
const id = ref(0);
const addToDo = () => {
  if(todo.value.trim() !== ''){
    todoList.value.push(todo.value)
    todo.value = ''
  } else {
    alert('пожалуйста введите текст');
  }
}
const deleteToDo = () => {
  todoList.value = [];     
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
