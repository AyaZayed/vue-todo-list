<script setup lang="ts">
import { ref, computed } from 'vue'

const newTask = ref('')

const todos = ref([
  { id: 1, text: 'Learn Vue', done: false },
  { id: 2, text: 'Build an app', done: false },
])

const addTodo = () => {
  if (newTask.value.trim() === '') return

  todos.value.push({
    id: Date.now(),
    text: newTask.value,
    done: false,
  })

  newTask.value = ''
}

const removeTodo = (id: number) => {
  todos.value = todos.value.filter((t) => t.id !== id)
}

const completedCount = computed(() => {
  return todos.value.filter((t) => t.done).length
})
</script>

<template>
  <main>
    <div class="app-container">
      <h1>Vue To-Do</h1>

      <div class="input-group">
        <input v-model="newTask" @keyup.enter="addTodo" placeholder="Add a task..." />
        <button @click="addTodo">Add</button>
      </div>

      <ul>
        <li v-for="todo in todos" :key="todo.id" class="todo-item">
          <div class="todo-text">
            <input type="checkbox" v-model="todo.done" />
            <span :class="{ completed: todo.done }">{{ todo.text }}</span>
          </div>
          <button @click="removeTodo(todo.id)" class="delete-btn">X</button>
        </li>
      </ul>

      <p v-if="todos.length === 0">No tasks yet!</p>
      <p v-else>Completed: {{ completedCount }} / {{ todos.length }}</p>
    </div>
  </main>
</template>

<style scoped>
main {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  background-color: #fbf8f8;
}

.app-container {
  min-width: 400px;
  width: 500px;
  padding: 30px 40px;
  border: 1px solid #ccc;
  border-radius: 15px;
  background-color: #fff;
  box-shadow: 0 1px 15px rgba(0, 0, 0, 0.1);
  background-color: white;
}

.app-container h1,
.app-container ul {
  margin-bottom: 1.5rem;
}

.input-group {
  display: flex;
  margin-bottom: 20px;
  width: 100%;
}

.input-group input {
  flex: 1;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 5px 0 0 5px;
}

.input-group button {
  padding: 10px 20px;
  border: 1px solid #ccc;
  border-radius: 0 5px 5px 0;
  background-image: linear-gradient(
    to right,
    #ff8177 0%,
    #ff867a 0%,
    #ff8c7f 21%,
    #f99185 52%,
    #cf556c 78%,
    #b12a5b 100%
  );
  cursor: pointer;
  font-weight: 600;
}

ul {
  list-style: none;
  padding: 0;
  margin: 0;
}

.todo-item {
  display: flex;
  align-items: center;
  margin-bottom: 10px;
  justify-content: space-between;
}

.todo-item input[type='checkbox'] {
  margin-right: 10px;
}

.completed {
  text-decoration: line-through;
}

.delete-btn {
  padding: 5px 10px;
  border: 2px solid #b12a5b;
  color: #b12a5b;
  cursor: pointer;
  border-radius: 50%;
  width: 30px;
  height: 30px;
  display: flex;
  justify-content: center;
  align-items: center;
  font-weight: 600;
  background-color: #fff;
}
</style>
