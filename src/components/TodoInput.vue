<template>
  <v-text-field
    :value="todoText"
    label="무엇을 해야 합니까?"
    @keyup.enter="submit(todoText)"
    @change="handleInputChange"
    solo
    required
  ></v-text-field>
</template>

<script>
  export default {
    name: 'TodoInput',
    methods: {
      submit() {
        this.handleSubmit(this.todoText);
      },
    },
    props: {
      todoText: String,
      handleSubmit: Function,
      handleInputChange: Function,
    },
  };
</script>

<style scoped>

</style>
