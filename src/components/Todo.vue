<template>
  <v-list-tile @click="() => {}">
    <v-list-tile-action>
      <v-checkbox
        color="indigo"
        v-model="todo.done"
        ref="done"
      ></v-checkbox>
    </v-list-tile-action>

    <v-list-tile-content @click.prevent="handleClick">
      <v-list-tile-title>{{todo.title}}</v-list-tile-title>
      <v-list-tile-sub-title>{{todo.created_at}}</v-list-tile-sub-title>
    </v-list-tile-content>

    <v-list-tile-action>
      <v-btn icon ripple @click="removeTodo(index)">
        <v-icon color="grey lighten-1">remove</v-icon>
      </v-btn>
    </v-list-tile-action>
  </v-list-tile>
</template>

<script>
  export default {
    name: 'Todo',
    props: {
      index: Number,
      todo: Object,
      removeTodo: Function,
    },
    methods: {
      handleClick() {
        this.todo.done = !this.todo.done;
      },
    },
  };
</script>

<style scoped lang="scss">
</style>
