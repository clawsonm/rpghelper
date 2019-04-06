<template>
  <ul class="players" v-if="players.length">
    <li v-for="player in players"
        is="Player"
        v-bind:player="player"
        v-bind:key="player.id">
    </li>
  </ul>
</template>

<script>
import Player from './Player.vue';

export default {
  name: 'PlayerList',
  props: ['players'],
  components: {
    Player,
  },
};
</script>
