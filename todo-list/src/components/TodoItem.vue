<template>
  <li class="flex items-center gap-2 px-3 py-2">
    <!-- 편집모드 -->
    <template v-if="todo.isEditing">
      <input
        v-model="todo.text"
        @keyup.enter="finishEdit"
        @blur="finishEdit"
        class="flex-1 border rounded px-2 py-1 focus:outline-none focus:ring-2 focus:ring-blue-400"
      />
    </template>
    <!-- 일반모드 -->
    <template v-else>
      <input type="checkbox" v-model="todo.done" />
      <span :class="{ done: todo.done }" class="flex-1 font-sans">{{ todo.text }}</span>
    </template>
    <button v-if="!todo.isEditing" @click="editTodo" class="text-sm text-blue-500 hover:underline">편집</button>
    <button @click="removeTodo" class="ml-auto text-sm text-red-500 hover:underline">X</button>
  </li>
</template>

<script setup>

const props = defineProps({ todo: Object });
const emit = defineEmits(["remove", "update"]);

// todo 수정
function editTodo() {
  props.todo.isEditing = true;
}

// todo 수정완료, props로 부모에서 Todo 객체를 받고 emit으로 삭제/수정 이벤트 전달
function finishEdit() {
  props.todo.isEditing = false;
  if (props.todo.text.trim() === "") {
    emit("remove");  // 자식 -> 부모 객체로 remove 전달
  } else {
    emit("update", props.todo); // 부모로부터 props를 통해 todo 객체를 받고 부모로 update 전달 
  }
}

// todo 삭제
function removeTodo() {
  emit("remove");
}
</script>

<style scoped>  
.done {
  text-decoration: line-through;
  color: #888;
}
</style>