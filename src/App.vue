<template>
  <div class="todo-app">
    <form @submit.prevent="addTodo" class="todo-form">
      <input v-model="newTodo.text" required placeholder="New todo" class="todo-input">
      <button type="submit" class="todo-button">Add Todo</button>
    </form>
    <ul class="todo-list">
      <li v-for="todo in todos" :key="todo.id" class="todo-item">
        <input type="checkbox" v-model="todo.done">
        <input v-model="todo.text" @blur="updateTodo" class="todo-text">
        <button @click="removeTodo(todo)" class="delete-button">X</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      todos: [
        { id: 1, text: "Memasak", done: false },
        { id: 2, text: "Membuat tugas", done: true },
        { id: 3, text: "Shalat", done: true },
        { id: 4, text: "Rapat", done: false },
        { id: 5, text: "Membaca buku selama 1 jam", done: false },
        { id: 6, text: "Jalan-jalan", done: true }
      ],
      newTodo: { text: "", done: false }
    };
  },
  methods: {
    addTodo() {
      if (this.newTodo.text.trim() !== "") {
        this.newTodo.id = this.todos.length + 1;
        this.todos.push({ ...this.newTodo });
        this.newTodo.text = "";
        this.newTodo.done = false;
      }
    },
    removeTodo(todo) {
      const index = this.todos.indexOf(todo);
      if (index !== -1) {
        this.todos.splice(index, 1);
      }
    },
    updateTodo() {
      // Optional: You can handle update logic here if needed
    }
  }
};
</script>

<style scoped>
.todo-app {
  max-width: 400px;
  margin: 20px auto;
}

.todo-form {
  display: flex;
  margin-bottom: 10px;
}

.todo-input {
  flex: 1;
  padding: 8px;
  border: 1px solid #ccc;
}

.todo-button {
  padding: 8px;
  border: none;
  background-color: #4caf50;
  color: white;
  cursor: pointer;
}

.todo-button:hover {
  background-color: #45a049;
}

.todo-list {
  list-style-type: none;
  padding: 0;
}

.todo-item {
  display: flex;
  align-items: center;
  margin-bottom: 5px;
}

.todo-text {
  flex: 1;
  padding: 5px;
}

.delete-button {
  padding: 5px;
  margin-left: 5px;
  background-color: #f44336;
  color: white;
  border: none;
  cursor: pointer;
}

.delete-button:hover {
  background-color: #d32f2f;
}
</style>
