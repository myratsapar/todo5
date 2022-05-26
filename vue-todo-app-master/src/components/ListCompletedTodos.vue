<template>
  <div>
    <h2 class="tasks">
      Completed Tasks
      <span class="meta">({{ todos.length }})</span>
    </h2>
    <v-container>
      <draggable v-model="draggableCards">
        <item-todo
          v-for="(todo, index) in todos"
          :todo.sync="todo"
          :index.sync="index"
          :key="todo.dateCreated"
          @delete-todo="deleteTodo"
        />
      </draggable>
    </v-container>
  </div>
</template>

<script type = "text/javascript" >
import ItemTodo from './ItemTodo';
import draggable from "vuedraggable";

export default {
  components: {
    draggable,
    ItemTodo,
  },
  props: {
    todos: {
      type: Array,
      default: function() {
        return []
      }
    }
  },
  methods: {
    deleteTodo(todo) {
      this.$emit('delete-todo', todo);
    }
  }
};
</script>
