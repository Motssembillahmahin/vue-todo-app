<template>
  <div id="app">
    <h1>My Vue Todo App</h1>

    <!-- Todo input form -->
    <div class="add-todo">
      <input
        type="text"
        v-model="newTodo"
        placeholder="What needs to be done?"
        @keyup.enter="addTodo"
      />
      <button @click="addTodo">Add Todo</button>
    </div>

    <!-- Todo list -->
    <ul class="todo-list" v-if="todos.length > 0">
      <li
        v-for="todo in todos"
        :key="todo.id"
        :class="{ completed: todo.completed }"
      >
        <input
          type="checkbox"
          :checked="todo.completed"
          @change="toggleTodo(todo.id)"
        />
        <span>{{ todo.text }}</span>
        <button class="delete-btn" @click="deleteTodo(todo.id)">×</button>
      </li>
    </ul>

    <p v-else>No todos yet. Add one above!</p>
  </div>
</template>

<script setup>
import { ref } from "vue";

// Reactive data
const todos = ref([
  { id: 1, text: "Learn Vue basics", completed: false },
  { id: 2, text: "Build a todo app", completed: true },
  { id: 3, text: "Master Vue components", completed: false },
]);

const newTodo = ref("");

// Methods
const addTodo = () => {
  if (newTodo.value.trim() === "") return;

  todos.value.push({
    id: Date.now(), // Simple ID generation
    text: newTodo.value,
    completed: false,
  });

  newTodo.value = ""; // Clear input
};

const deleteTodo = (id) => {
  todos.value = todos.value.filter((t) => t.id !== id);
};
</script>

<style>
#app {
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
  font-family: Arial, sans-serif;
}

.add-todo {
  display: flex;
  gap: 10px;
  margin-bottom: 20px;
}

.add-todo input {
  flex-grow: 1;
  padding: 10px;
  font-size: 16px;
  border: 1px solid #ddd;
  border-radius: 4px;
}

.add-todo button {
  padding: 10px 20px;
  background-color: #42b883;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 16px;
}

.todo-list {
  list-style: none;
  padding: 0;
}

.todo-list li {
  display: flex;
  align-items: center;
  gap: 10px;
  padding: 12px;
  border: 1px solid #eee;
  margin-bottom: 8px;
  border-radius: 4px;
  background-color: #f9f9f9;
  transition: all 0.3s ease;
}

.todo-list li.completed {
  background-color: #e8f5e9;
}

.todo-list li.completed span {
  text-decoration: line-through;
  color: #888;
}

.todo-list input[type="checkbox"] {
  width: 18px;
  height: 18px;
  cursor: pointer;
}
.delete-btn {
  margin-left: auto;
  background: none;
  border: none;
  color: #ff6b6b;
  font-size: 24px;
  cursor: pointer;
  width: 30px;
  height: 30px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
}

.delete-btn:hover {
  background-color: #ffeaea;
}
</style>
