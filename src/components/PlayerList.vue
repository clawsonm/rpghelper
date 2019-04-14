<template>
  <ul class="players" v-if="players.length">
    <li v-for="player in players"
        is="Player"
        :player="player"
        :key="player.id"
        @click-remove-player="$emit('remove-player', player.id)">
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

<style scoped>
.players {
  padding-left: 0;
}
</style>
