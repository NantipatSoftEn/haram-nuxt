<template>
  <ul>
    <li v-for="todo in todos" :key="todo.text">
      <input :checked="todo.done" @change="toggle(todo)" type="checkbox" />
      <span :class="{ done: todo.done }">{{ todo.text }}</span>
    </li>
    <li>
      <input @keyup.enter="addTodo" placeholder="What needs to be done?" />
    </li>
  </ul>
</template>

<script>
import { mapMutations, mapGetters, mapActions } from "vuex";

export default {
  computed: {
    // todos() {
    //   return this.$store.state.todos.list;
    // }
    ...mapGetters({ todos: "todos/lists" })
  },
  methods: {
    // addTodo(e) {
    //   this.$store.commit("todos/add", e.target.value);
    //   e.target.value = "";
    // },
    ...mapActions({
      addTodo: "todos/addTodo"
    }),
    ...mapMutations({
      toggle: "todos/toggle"
    })
  }
};
</script>

<style>
.done {
  text-decoration: line-through;
}
</style>
