<template>
  <v-text-field
    v-model="todoText"
    label="무엇을 해야 합니까?"
    @keyup.enter="submit()"
    solo
    required
  ></v-text-field>
</template>

<script>
  export default {
    name: 'TodoInput',
    data: () => ({
      todoText: '',
    }),
    methods: {
      submit() {
        this.handleSubmit(this.todoText);
        this.todoText = '';
      },
    },
    props: {
      handleSubmit: Function,
    },
    method: {},
  };
</script>

<style scoped>

</style>
