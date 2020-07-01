<template>
  <div class="todo-item" :class="{ 'is-complete': todo.completed }">
    <input type="checkbox" v-on:change="markComplete" />
    <p>{{ todo.title }}</p>
    <button @click="$emit('delete-todo', todo.id)" class="del">x</button>
  </div>
</template>

<script>
export default {
  name: "TodoItem",
  props: ["todo"],
  methods: {
    markComplete() {
      this.todo.completed = !this.todo.completed;
    }
  }
};
</script>

<style lang="scss" scoped>
.todo-item {
  background: #f4f4f4;
  padding: 1rem;
  border-bottom: 1px #ccc dotted;

  display: flex;
  align-items: center;
  justify-content: center;

  input {
    margin-right: .5rem;
  }

  button {
    background: #ff0000;
    color: #fff;
    border: none;
    padding: 0.5rem 0.75rem;
    border-radius: 50%;
    cursor: pointer;
    margin-left: auto;
    outline: none;
  }
}

.is-complete {
  text-decoration: line-through;
}
</style>
