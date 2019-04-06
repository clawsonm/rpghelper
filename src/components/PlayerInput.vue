<template>
  <form v-on:submit.prevent="onSubmit">
    <input type="text" v-model="player.name">
    <input type="number" v-model="player.dex">
    <button>Add Player</button>
  </form>
</template>

<script>
export default {
  name: 'PlayerInput',
  data() {
    return {
      player: {
        name: '',
        dex: 0,
        initiative: -1,
      },
    };
  },
  methods: {
    onSubmit() {
      this.$emit('add-player', this.player);
      this.player.name = '';
      this.player.initiative = -1;
      this.player.dex = 0;
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
