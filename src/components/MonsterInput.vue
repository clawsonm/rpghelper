<template>
  <form v-on:submit.prevent="onSubmit">
    <input type="text" v-model="monster.name">
    <input type="number" v-model="monster.dex">
    <button>Add Monster</button>
  </form>
</template>

<script>
export default {
  name: 'MonsterInput',
  data() {
    return {
      monster: {
        name: '',
        dex: 0,
      },
    };
  },
  methods: {
    onSubmit() {
      this.$emit('add-monster', this.monster);
      this.monster.name = '';
      this.monster.dex = 0;
    },
  },
};
</script>

<style scoped>
  input[type="number"]
  {
    min-height: 32px;
  }
</style>
