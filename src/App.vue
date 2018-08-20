<template>
  <v-app id="inspire">
    <v-layout align-center justify-center>
      <h1 class="display-3 font-weight-thin pt-5 pb-4">TODO</h1>
    </v-layout>
    <v-container fluid fill-height>
      <v-layout justify-center>
        <v-flex xs12 sm8 md6>
          <TodoList />
        </v-flex>
      </v-layout>
    </v-container>
  </v-app>
</template>

<script>
import TodoList from './components/TodoList.vue';

export default {
  components: { TodoList },
  data: () => ({}),
  props: {},
};
</script>
