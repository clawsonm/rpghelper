<template>
  <form v-on:submit.prevent="onSubmit" class="monster-form">
    <input type="text" v-model="monster.name" placeholder="Identifier &amp; Dex">
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
    width: 4rem;
  }
  .monster-form {
    margin-top: 20px;
  }
  input, button {
    margin: 0 5px 0 5px;
  }
</style>
