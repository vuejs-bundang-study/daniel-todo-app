<template>
  <v-app id="inspire">
    <v-layout align-center justify-center>
      <h1 class="display-3 font-weight-thin pt-5 pb-4">TODO</h1>
    </v-layout>
    <v-container fluid fill-height>
      <v-layout justify-center>
        <v-flex xs12 sm8 md6>
          <TodoInput
            :handle-input-change="handleInputChange"
            :handle-submit="handleSubmit"
            :todo-text="todoText"
          />
          <TodoList
            :todo-list="todoList"
            :change-tab="changeTab"
            :activated-tab="activatedTab"
            :remove="remove"
          />
        </v-flex>
      </v-layout>
    </v-container>
    <v-snackbar
      v-model="snackbarShow"
      bottom
      left
      :timeout="3000"
    >
      {{ snackbarMessage }}
      <v-btn
        color="pink"
        flat
        @click="snackbarShow = false"
      >
        Close
      </v-btn>
    </v-snackbar>
  </v-app>
</template>

<script>
  import moment from 'moment';
  import shortid from 'shortid';
  import TodoInput from './components/TodoInput.vue';
  import TodoList from './components/TodoList.vue';

  export default {
    components: { TodoInput, TodoList },
    data: () => ({
      activatedTab: 'ALL',
      todoText: '',
      todoList: [],
      snackbarShow: false,
      snackbarMessage: '',
    }),
    methods: {
      handleInputChange(value) {
          this.todoText = value;
      },
      handleSubmit(todoText) {
        if (!/.+/.test(todoText)) {
          this.showMessage('한 글자 이상 입력하세요');
          return;
        }
        this.todoText = '';
        const todo = {
          id: shortid.generate(),
          title: todoText,
          created_at: moment()
            .format('YYYY-MM-DD HH:mm:ss'),
          done: false,
        };
        this.todoList.push(todo);
        this.save();
      },
      remove(index) {
        this.todoList.splice(index, 1);
        this.save();
      },
      save() {
        localStorage.setItem('todo', JSON.stringify(this.todoList));
      },
      load() {
        const store = localStorage.getItem('todo');
        this.todoList = JSON.parse(store) || [];
      },
      showMessage(message) {
        this.snackbarMessage = message;
        this.snackbarShow = true;
      },
      changeTab(tab) {
        this.activatedTab = tab;
      },
    },
    props: {},
    mounted() {
      this.load();
    },
  };
</script>
