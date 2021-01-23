<template>
  <div>
    <h2>Todos</h2>
    <AddTodo @addTodo="addTodo" />
    <select v-model="filter">
        <option value="all">Show all</option>
        <option value="complited">Complited</option>
        <option value="not-complited">Not complited</option>
    </select>
    <hr />
    <Loader v-if="loading" />
    <TodoList 
        v-bind:todos="filteredTodo" 
        @remove-todo="removeTodo"
        v-else-if = "filteredTodo.length"
    />
    <p v-else>
        Nothing here!
    </p>

  
    <hr>
    <router-link to="/">go to to home</router-link>
  </div>
</template>

<script>
import TodoList from "@/components/TodoList.vue";
import AddTodo from "@/components/AddTodo.vue";
import Loader from "@/components/Loader.vue";
export default {
  name: "app",
  data() {
    return {
      todos: JSON.parse(localStorage.getItem('todos')),
      loading: true,
      filter: 'all'
    };
  },
  components: {
    TodoList,
    AddTodo,
    Loader
  },
    computed: {
      filteredTodo() {
          if (this.filter === "all") {
              return this.todos;
          }else if (this.filter ==='complited') {
              return this.todos.filter(t => t.completed)
          }else if (this.filter === "not-complited") {
              return this.todos.filter(t => !t.completed)
          }
          return 'all';
      }  
    },
  methods: {
    removeTodo(id) {
      this.todos = this.todos.filter((el) => el.id !== id);
      localStorage.setItem('todos', JSON.stringify(this.todos));
    },
    addTodo(todo) {
      this.todos.push(todo);
      localStorage.setItem('todos', JSON.stringify(this.todos));
    },
  },
  mounted() {

    setTimeout(() => {
        this.loading = false;
    }, 500);
  }
};
</script>