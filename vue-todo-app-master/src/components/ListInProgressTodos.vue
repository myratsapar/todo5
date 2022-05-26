<template>
  <div>
    <h2 class="tasks">
      Tasks In Progress
      <span class="meta">({{ todos.length }})</span>
    </h2>
    <v-container>
      <draggable v-model="draggableCards">
        <item-todo
          v-for="(todo, index) in todos"
          :todo.sync="todo"
          :index.sync="index"
          :key="todo.dateCreated"
          :init-collapsed="false"
          @delete-todo="deleteTodo"
          @complete-todo="completeTodo"
          @edit-todo="editTodo"
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
    completeTodo(todo) {
      this.$emit('complete-todo', todo);
    },
    deleteTodo(todo) {
      this.$emit('delete-todo', todo);
    },
    editTodo(todo) {
      this.$emit('edit-todo', todo);
    }
  }
};
</script>
<style>
.{
  cursor: pointer;
}
</style>
