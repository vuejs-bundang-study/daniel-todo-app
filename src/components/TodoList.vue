<template>
  <div>
    <v-card v-if="todoList.length > 0">
      <TodoTab
        :change-tab="changeTab"
      />
      <v-list
        subheader
        two-line
      >
        <Todo
          v-for="(todo, index) in todos"
          :key="todo.id"
          :index="index"
          :todo="todo"
          :remove-todo="remove"
        />
      </v-list>
    </v-card>
  </div>
</template>

<script>
  import Todo from './Todo.vue';
  import TodoTab from './TodoTab.vue';

  export default {
    props: {
      todoList: Array,
      changeTab: Function,
      activatedTab: String,
      remove: Function,
    },
    components: { TodoTab, Todo },
    computed: {
      todos() {
        switch (this.activatedTab) {
        case 'ALL': {
          return this.todoList;
        }
        case 'TODO': {
          return this.todoList.filter(todo => !todo.done);
        }
        case 'DONE': {
          return this.todoList.filter(todo => todo.done);
        }
        default:
          return [];
        }
      },
    },
  };
</script>

<style scoped>
</style>
