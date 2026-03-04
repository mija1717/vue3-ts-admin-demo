<template>
  <div class="todo-list">
    <h2>Todo List</h2>
    <div v-for="todo in todoList" :key="todo.id">
      <input type="checkbox" v-model="todo.completed" />
      <span>&nbsp;{{ todo.text }}&nbsp;</span>
      <button @click="deleteTodo(todo.id)">del</button>
    </div>
    <div>
      <input type="text" v-model="newTodoText" placeholder="输入待办事项..." />
      <button @click="addTodo">添加</button>
    </div>
    <div>
      <p>已完成: {{ completedCount }}</p>
      <p>未完成: {{ uncompletedCount }}</p>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, computed } from "vue";

interface TodoItem {
  id: number;
  text: string;
  completed: boolean;
  createdAt: Date;
}

const todoList = ref<TodoItem[]>([
  {
    id: 1,
    text: "TodoItem1",
    completed: false,
    createdAt: new Date(),
  },
]);

const newTodoText = ref("");

function addTodo(): void {
  if (!newTodoText.value.trim()) {
    alert("请输入todo事项");
    return;
  }
  todoList.value.push({
    id: Date.now(),
    text: newTodoText.value.trim(),
    completed: false,
    createdAt: new Date(),
  });
  newTodoText.value = "";
}

function deleteTodo(id: number) {
  const todoIndex = todoList.value.findIndex((todo) => todo.id === id);
  if (todoIndex !== -1) {
    todoList.value.splice(todoIndex, 1);
  }
}

const completedCount = computed(() => {
  return todoList.value.filter((todo) => todo.completed).length;
});

const uncompletedCount = computed(() => {
  return todoList.value.filter((todo) => !todo.completed).length;
});
</script>
