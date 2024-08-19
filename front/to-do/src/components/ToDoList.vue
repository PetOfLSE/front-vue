<template>
  <ul>
    <li v-for="(todo, index) in localTodos" :key="index">
      <input type="checkbox" v-model="todo.completed" @change="saveTodos" />
      <span :class="{ completed: todo.completed }">{{ todo.text }}</span>
      <button @click="removeTodo(index)">삭제</button>
    </li>
  </ul>
</template>

<script>
export default {
  name: 'ToDoList',
  props: {
    todos: {
      type: Array,
      required: true
    }
  },
  data() {
    return {
      localTodos: [...this.todos] // todos의 복사본을 로컬 상태로 저장
    };
  },
  watch: {
    todos(newTodos) {
      this.localTodos = [...newTodos];
    }
  },
  methods: {
    removeTodo(index) {
      this.localTodos.splice(index, 1);
      this.$emit('remove-todo', index);
    },
    saveTodos() {
      this.$emit('save-todos', this.localTodos);
    }
  }
};
</script>

<style>
.completed {
  text-decoration: line-through;
  color: grey;
}
</style>
