<template>
  <v-list
          subheader
          two-line
  >
    <Todo
      v-for="todo in todoList"
      :key="todo.id"
      :todo="todo"
    />
  </v-list>
</template>

<script>
import Todo from './Todo.vue';

export default {
  components: { Todo },
  data: () => ({
    todoList: [
      {
        id: 1,
        title: '코딩하기',
        created_at: '2018-08-20',
        done: false,
      },
      {
        id: 2,
        title: '장보기',
        created_at: '2018-08-20',
        done: false,
      },
      {
        id: 3,
        title: '청소하기',
        created_at: '2018-08-20',
        done: false,
      },
    ],
  }),
  props: {},
};
</script>

<style scoped>

</style>
