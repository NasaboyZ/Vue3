<template>
  <main class="p-4 max-w-md mx-auto">
    <h1 class="text-2xl font-bold mb-4">📝 Meine To-Do Liste</h1>

    <form @submit.prevent="addTodo" class="flex gap-2 mb-4 mt-4">
      <input
        v-model="newTodo"
        class="flex gap-4 mb-4 mt-4 border p-2 flex-1"
        placeholder="Neue Aufgabe eingeben..."
      />
      <button class="bg-blue-500 text-white px-4 py-2 rounded">
        Hinzufügen
      </button>
    </form>

    <ul class="list-none">
      <li
        v-for="(todo, index) in todos"
        :key="index"
        class="flex items-center justify-between mb-2"
      >
        <label class="flex items-center gap-2">
          <input type="checkbox" v-model="todo.done" />
          <span :class="{ 'line-through text-gray-400': todo.done }">{{
            todo.text
          }}</span>
        </label>
        <button
          @click="removeTodo(index)"
          class="text-red-500 hover:underline px-4 py-2 rounded"
        >
          Entfernen
        </button>
      </li>
    </ul>

    <p class="mt-4 text-sm text-gray-600">
      {{ openCount }} offen / {{ todos.length }} total
    </p>
  </main>
</template>

<script setup>
import { ref, computed } from "vue";

const newTodo = ref("");
const todos = ref([]);

const addTodo = () => {
  if (newTodo.value.trim() === "") return;
  todos.value.push({ text: newTodo.value, done: false });
  newTodo.value = "";
};

const removeTodo = (index) => {
  todos.value.splice(index, 1);
};

const openCount = computed(() => todos.value.filter((t) => !t.done).length);
</script>

<style scoped>
body {
  font-family: sans-serif;
}
</style>
