<template>
  <div class="max-w-md mx-auto mt-10 p-6 bg-white shadow-lg rounded-2xl">
    <h3 class="text-2xl font-bold text-black-600 mb-4">☑️ ToDoList</h3>

    <!-- 전체/남은건수 / 오늘날짜 -->
    <div class="flex justify-between items-center text-gray-500 text-sm mb-4">
      <div>전체: {{ todos.length }} / 남은 개수: {{ remainingTodos }}</div>
      <div>{{ today }}</div>
    </div>

    <!-- 입력 -->
    <TodoInput @add-todo="addTodo" />

    <!-- Todo 목록 -->
    <ul class="divide-y divide-gray-300">
      <TodoItem
        v-for="(todo, index) in todos"
        :key="index"
        :todo="todo"
        @remove="removeTodo(index)"
        @update="updateTodo"
      />
    </ul>
  </div>
</template>

<script setup>
import { reactive, computed } from "vue";
import TodoInput from "./TodoInput.vue";
import TodoItem from "./TodoItem.vue";

// todos reactive 배열 선언
const todos = reactive([]);

// 오늘 날짜
const today = new Date().toLocaleDateString("ko-KR", {
  year: "numeric",
  month: "long",
  day: "numeric"
});

// 남은 Todo
const remainingTodos = computed(() => todos.filter(todo => !todo.done).length);

// Todo 추가
function addTodo(text) {
  todos.push({ text, done: false, isEditing: false });
}

// Todo 삭제
function removeTodo(index) {
  todos.splice(index, 1);
}

function updateTodo(updatedTodo) {
  // reactive 배열이라 자동 반응됨, 필요 시 추가 로직
}
</script>
