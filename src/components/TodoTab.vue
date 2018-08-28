<template>
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
</template>

<script>
  export default {
    name: 'TodoTab',
    props: {
      changeTab: Function,
    },
  };
</script>

<style scoped>

</style>
