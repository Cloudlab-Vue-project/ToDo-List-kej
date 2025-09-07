<template>
  <div class="min-h-screen bg-gray-100 p-6">
    <div class="max-w-md mx-auto mt-10 p-6 bg-white shadow-lg rounded-2xl">
      <h3 class="text-2xl font-bold text-black-600 mb-4">☑️ ToDoList</h3>
      <!-- 전체/남은건수 / 오늘날짜 표기 -->
      <div class="flex justify-between items-center text-gray-500 text-sm mb-4">
        <div>
          전체: {{todos.length}} 개 / 남은 건: {{ remainingTodos }} 개
        </div>
        <div>
          {{ today }}
        </div>
      </div>
      <!-- 오늘 할 일 목록 표기 -->
      <div class="flex gap-2 mb-4">
      <input v-model="newTodo" @keyup.enter="addTodo" placeholder="할 일을 입력하세요" class="flex-1 border rounded-lg px-3 py-2 focus:outline-none focus:ring-2 focus:ring-blue-400"></input> 
      <button @click="addTodo" class="bg-blue-500 text-white px-4 py-2 rounded-lg hover:bg-gray-600 transition">+</button>
      </div>
      <!-- 입력된 할 일 표기 -->
      <ul class="divide-y divide-gray-300">
        <li v-for="(todo, index) in todos" :key="index" class="flex items-center gap-2 px-3 py-2">
        <input type="checkbox" v-model="todo.done"></input>
          <span :class="{done: todo.done}" class="font-sans">{{ todo.text }} </span>

          <button @click="removeTodo(index)" class="ml-auto text-sm text-red-500 hover:underline">X</button>
        </li>
      </ul>
    </div>
  </div>
</template>

<script setup>
import {ref, reactive, computed} from "vue";

const newTodo = ref(""); // 단일 입력값
const todos = reactive([]); //Todo 배열 (reactive로 관리)

// 오늘 날짜
const today = new Date().toLocaleDateString("ko-KR", {
  year: "numeric",
  month: "long",
  day: "numeric"
});

// 남은 할 일 계산
const remainingTodos = computed(() => {
  return todos.filter(todo => !todo.done).length;
});

// Todo 추가
function addTodo() {
  if(newTodo.value.trim() == "") return; 

  todos.push({text: newTodo.value, done: false});
  newTodo.value="";
}

// Todo 삭제
function removeTodo(index) {
  todos.splice(index, 1);
}
</script>

<style scoped>
.done {
  text-decoration: line-through;
  color: #888;
}
</style>
