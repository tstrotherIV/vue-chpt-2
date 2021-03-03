<template>
  <div>
    <h3>ToDo List</h3>
    <h5>{{ itemsRemaining }}</h5>
    <div v-for="item in todos" :key="item.id">
      <todo-item :todo="item" @status-change="handleStatusChange" />
    </div>
  </div>
</template>

<script>
import { todoItems } from "../data";
import TodoItem from "./TodoItem";

export default {
  components: { TodoItem },
  methods: {
    handleStatusChange(item) {
      item.complete = !item.complete;
      console.log(item);
    },
  },
  data() {
    return {
      todos: [...todoItems],
    };
  },
  computed: {
    itemsRemaining() {
      const remaining = this.todos.filter((t) => !t.complete);
      if (remaining.length == 1) {
        return "There is 1 item left to do today";
      } else if ( remaining.length == 0 ) {
        return "There is nothing left to do today!"
      }
      return `There are ${remaining.length} items left to do today`;
    },
  },
};
</script>

<style></style>
