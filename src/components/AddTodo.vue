<template>
  <form @submit.prevent="onSubmit">
    <input type="text" v-model="title" />
    <!-- модель - при изменении инпута
    значение попадает в data.title -->
    <button type="submit">Add</button>
  </form>
</template>

<script>
export default {
  data() {
    return {
      title: "",
    };
  },
  methods: {
    onSubmit() {
      if (this.title.trim()) {
        const newTodo = {
          id: Date.now(),
          title: this.title,
          completed: false,
        };
        this.$emit("addTodo", newTodo);
        this.title = "";
      }
    },
  },
};
</script>

<style scoped>
input {
  width: 50%;
}
</style>