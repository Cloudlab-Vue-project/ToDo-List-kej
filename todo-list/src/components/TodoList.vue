<template>
  <div class="todo-container">
    <h3>ToDoList</h3>
    <input v-model="newTodo" @keyup.enter="addTodo" placeholder="입력"></input>
    <button @click="addTodo">추가</button>
    
     <ul>
      <li v-for="(todo, index) in todos" :key="index" :class="{done: todo.done}">
      {{ todo.text }}
        <button @click="removeTodo(index)">삭제</button>
      </li>
     </ul>
  </div>
</template>

<script setup>
import {ref} from "vue";

const newTodo = ref("");
const todos = ref([]);

// [Todo 추가 Start]
function addTodo() {
  if(newTodo.value.trim() == "") return;

  todos.value.push({text: newTodo.value, done: false});
  newTodo.value="";
}

// [Todo 삭제 Start]
function removeTodo(index) {
  todos.value.splice(index, 1);
}
</script>

<style scoped>
.todo-container {
  max-width: 400px;
  margin: 50px auto;
  text-align: center;
}
ul {
  list-style: none;
  padding: 0;
}
li {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin: 5px 0;
}
.done {
  text-decoration: line-through;
  color: gray;
}
</style>