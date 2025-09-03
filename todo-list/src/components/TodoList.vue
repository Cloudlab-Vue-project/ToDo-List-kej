<template>
  <div class="max-w-md mx-auto mt-10 p-6 bg-white shadow-lg rounded-2xl">
    <h3 class="text-2xl font-bold text-blue-600 mb-4">ToDoList</h3>

    <div class="flex gap-2 mb-4">
    <input v-model="newTodo" @keyup.enter="addTodo" placeholder="할 일을 입력하세요" class="flex-1 border rounded-lg px-3 py-2 focus:outline-none focus:ring-2 focus:ring-blue-400"></input> 
    <button @click="addTodo" class="bg-gray-500 text-white px-4 py-2 rounded-lg hover:bg-blue-600 transition">추가</button>
    </div>
    
     <ul class="space-y-2">
      <li v-for="(todo, index) in todos" :key="index" class="flex items-center gap-2 border px-3 py-2 rounded-lg">
      <!-- 체크박스 추가 -->
      <input type="checkbox" v-model="todo.done"></input>
        <span>{{ todo.text }} </span>
        <button @click="removeTodo(index)" class="ml-auto text-sm text-red-500 hover:underline">X</button>
      </li>
     </ul>
  </div>
</template>

<script setup>
import {ref} from "vue";

const newTodo = ref("");  // ref는 Vue의 반응형 변수(문자열상태)
const todos = ref([]);  // 배열상태

// [Todo 추가 Start]
function addTodo() {
  if(newTodo.value.trim() == "") return;  // 빈 문자열이면 추가x

  todos.value.push({text: newTodo.value, done: false});  // todos 배열에 객체 추가
  newTodo.value="";  // 입력창 초기화
}

// [Todo 삭제 Start]
function removeTodo(index) {
  todos.value.splice(index, 1);  // 해당 index 항목 제거
}
</script>
