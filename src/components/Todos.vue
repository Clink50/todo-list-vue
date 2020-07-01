<template>
  <div>
    <div v-for="todo in todos" :key="todo.id">
      <TodoItem :todo="todo" v-on:delete-todo="$emit('delete-todo', todo.id)" />
    </div>
  </div>
</template>

<script>
import TodoItem from './TodoItem';

export default {
  name: 'Todos',
  props: ['todos'],
  components: {
    TodoItem,
  },
}
</script>

<style lang="scss" scoped>

</style>
