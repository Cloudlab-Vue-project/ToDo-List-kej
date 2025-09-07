<template>
  <div class="flex gap-2 mb-4">
    <input
      v-model="newTodo"
      @keyup.enter="add"
      placeholder="할 일을 입력하세요"
      class="flex-1 border rounded-lg px-3 py-2 focus:outline-none focus:ring-2 focus:ring-blue-400"
    />
    <button @click="add" class="bg-blue-500 text-white px-4 py-2 rounded-lg hover:bg-gray-600 transition">+</button>
  </div>
</template>

<script setup>
import { ref } from "vue";

const newTodo = ref("");
const emit = defineEmits(["add-todo"]);  // 입력창과 + 버튼, emit으로 부모에게 전달

function add() {
  if (newTodo.value.trim() === "") return;  // 빈 배열이면 return ;
  emit("add-todo", newTodo.value);
  newTodo.value = "";
}
</script>
