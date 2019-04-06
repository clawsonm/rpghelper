<template>
  <div>
    {{ player.name }},
    Dex: {{ player.dex }},
    Initiative: <input type="number" v-model="player.initiative">
  </div>
</template>

<script>
export default {
  name: 'Player',
  props: ['player'],
};
</script>

<style scoped>
  input[type="number"]
  {
    min-height: 32px;
  }
</style>
