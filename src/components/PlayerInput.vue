<template>
  <form v-on:submit.prevent="onSubmit" class="player-form">
    <input type="text" v-model="player.name" placeholder="Name &amp; Dex">
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
        initiative: 10,
      },
    };
  },
  methods: {
    onSubmit() {
      this.$emit('add-player', this.player);
      this.player.name = '';
      this.player.initiative = 10;
      this.player.dex = 0;
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
  .player-form {
    margin-top: 20px;
  }
  input, button {
    margin: 0 5px 0 5px;
  }
</style>
