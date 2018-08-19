<template>
  <v-list-tile @click="() => {}">
    <v-list-tile-action>
      <v-checkbox
          v-model="todo.done"
      ></v-checkbox>
    </v-list-tile-action>

    <v-list-tile-content @click.prevent="">
      <v-list-tile-title>{{todo.title}}</v-list-tile-title>
      <v-list-tile-sub-title>{{todo.created_at}}</v-list-tile-sub-title>
    </v-list-tile-content>
  </v-list-tile>
</template>

<script>
export default {
  name: 'Todo',
  props: {
    todo: Object,
  },
};
</script>

<style scoped lang="scss">
</style>
