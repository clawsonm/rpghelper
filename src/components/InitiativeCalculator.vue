<template>
  <ul class="initiative">
    <li v-for="char in sortedPlayersAndMonster" v-bind:key="char.type + char.id">
      {{ char.name }} {{ char.initiative }}
    </li>
  </ul>
</template>

<script>
export default {
  props: ['players', 'monsters'],
  computed: {
    sortedPlayersAndMonster() {
      return [...this.players, ...this.monsters].sort((first, second) => {
        if (Number(first.initiative) > Number(second.initiative)) {
          return -1;
        }
        if (Number(first.initiative) < Number(second.initiative)) {
          return 1;
        }
        // at this point initiatives are equal
        if (Number(first.dex) > Number(second.dex)) {
          return -1;
        }
        if (Number(first.dex) < Number(second.dex)) {
          return 1;
        }
        // at this point initiative and dex are equal
        // move players ahead of monsters
        if (first.type === 'monster' && second.type === 'player') {
          return 1;
        }
        return 0;
      });
    },
  },
};
</script>
