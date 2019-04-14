<template>
  <li>
    <div class="name">
      {{ player.name }}
    </div>
    <div class="dex">
      <strong>Dex</strong>&nbsp;{{ player.dex }}
    </div>
    <div>
      <label :for="player.type + player.id + 'initiative'">Initiative</label>
      <input
        :name="player.type + player.id + 'initiative'"
        type="number"
        v-model="player.initiative">
    </div>
    <button @click="$emit('click-remove-player')">X</button>
  </li>
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
    width: 4rem;
  }
  li {
    display: inline-flex;
    align-items: center;
    justify-content: space-around;
    list-style: none;
    width: 80%;
  }
  input, button {
    margin: 0 5px 0 5px;
  }
  .name {
    flex-basis: 20%;
  }
  label {
    font-weight: bold;
  }
</style>
