<template>
  <div>
    <v-text-field
      v-model="todoText"
      label="무엇을 해야 합니까?"
      v-on:keyup.enter="submit"
      solo
      required
    ></v-text-field>
    <v-card v-if="todoList.length > 0">
      <v-tabs fixed-tabs slider-color="indigo">
        <v-tab @click="changeTab('ALL')">
          ALL
        </v-tab>
        <v-tab @click="changeTab('TODO')">
          TODO
        </v-tab>
        <v-tab @click="changeTab('DONE')">
          DONE
        </v-tab>
      </v-tabs>
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
  </div>
</template>

<script>
  import moment from 'moment';
  import shortid from 'shortid';
  import Todo from './Todo.vue';

  export default {
    components: { Todo },
    data: () => ({
      activatedTab: 'ALL',
      todoText: '',
      todoList: [],
      snackbarShow: false,
      snackbarMessage: '',
    }),
    methods: {
      submit() {
        if (!/.+/.test(this.todoText)) {
          this.showMessage('한 글자 이상 입력하세요');
          return;
        }
        const todo = {
          id: shortid.generate(),
          title: this.todoText,
          created_at: moment()
            .format('YYYY-MM-DD HH:mm:ss'),
          done: false,
        };
        this.todoList.push(todo);
        this.todoText = '';
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
    props: {},
    mounted() {
      this.load();
    },
  };
</script>

<style scoped>
</style>
