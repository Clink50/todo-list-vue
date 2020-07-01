<template>
  <div id="app">
    <AddTodo v-on:add-todo="addTodo" />
    <Todos :todos="todos" v-on:delete-todo="deleteTodo" />
  </div>
</template>

<script>
import Todos from "../components/Todos";
import AddTodo from "../components/AddTodo";

export default {
  name: "Home",
  components: {
    Todos,
    AddTodo
  },
  data() {
    return {
      todos: []
    };
  },
  methods: {
    async deleteTodo(id) {
      await fetch(`https://jsonplaceholder.typicode.com/todos/${id}`, {
        method: "DELETE",
      });
      
      this.todos = this.todos.filter(todo => todo.id !== id);
    },
    async addTodo(newTodo) {
      const { title, completed } = newTodo;
      console.log(JSON.stringify({ title, completed }));
      const res = await fetch("https://jsonplaceholder.typicode.com/todos", {
        method: "POST",
        body: JSON.stringify({
          title,
          completed
        }),
        headers: {
          "Content-type": "application/json; charset=UTF-8",
        },
      });
      const createdTodo = await res.json();
      this.todos = [...this.todos, createdTodo];
    }
  },
  async created() {
    const res = await fetch(
      "https://jsonplaceholder.typicode.com/todos?_limit=5"
    );
    const todos = await res.json();
    this.todos = todos;
  }
};
</script>

<style lang="scss">
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

html,
body {
  font-size: 16px;
  font-family: Arial, Helvetica, sans-serif;
  line-height: 1.4;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}

.btn {
  display: inline-block;
  border: none;
  background: #555;
  color: #fff;
  padding: 0.7rem 2rem;
  cursor: pointer;

  &:hover {
    background: #666;
  }
}
</style>
