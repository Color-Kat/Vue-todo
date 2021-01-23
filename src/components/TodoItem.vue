<template>
  <li>
    <span v-bind:class="{ done: todo.completed }">
      <input type="checkbox" v-on:change="todo.completed = !todo.completed" />
      <strong>{{ index + 1 }}</strong>
      {{ todo.title | upperCase }}
    </span>
    <button class="delete-btn" v-on:click="$emit('remove-todo', todo.id)">
      &times;
    </button>
  </li>
</template>

<script>
export default {
  name: "todoItem",
  props: {
    todo: {
      type: Object,
      required: true,
    },
    index: Number,
  },
  filters: {
    upperCase(value) {
      return value.toUpperCase();
    }
  }
};
</script>

<style scoped>
li {
  border: 1px solid rgb(80, 80, 80);
  margin-bottom: 1rem;
  display: flex;
  justify-content: space-between;
  padding: 0.5rem 2rem;
}
.delete-btn {
  background: #c91c1c;
  border: none;
  outline: none;
  border-radius: 50%;
  color: #fff;
  font-weight: bold;
}
.done {
  text-decoration: line-through;
}
input {
  margin-right: 1rem;
}
</style>

