<template>
  <div>
    <h2>Players</h2>
    <PlayerList v-bind:players="players" />
    <PlayerInput v-on:add-player="onAddPlayer" />
    <h2>Monsters</h2>
    <MonsterList v-bind:monsters="monsters" />
    <MonsterInput v-on:add-monster="onAddMonster" />
    <h2>Initiative Calc</h2>
    <InitiativeCalculator v-bind:players="players" v-bind:monsters="monsters" />
  </div>
</template>

<script>
import PlayerList from './PlayerList.vue';
import PlayerInput from './PlayerInput.vue';
import MonsterList from './MonsterList.vue';
import MonsterInput from './MonsterInput.vue';
import InitiativeCalculator from './InitiativeCalculator.vue';

export default {
  name: 'InitiativeApp',
  data() {
    return {
      players: [],
      monsters: [],
    };
  },
  components: {
    PlayerList,
    PlayerInput,
    MonsterList,
    MonsterInput,
    InitiativeCalculator,
  },
  methods: {
    onAddPlayer(player) {
      const id = this.players.length > 0 ? this.players[this.players.length - 1].id + 1 : 1;
      this.players.push({ ...player, id, type: 'player' });
    },
    onAddMonster(monster) {
      const id = this.monsters.length > 0 ? this.monsters[this.monsters.length - 1].id + 1 : 1;
      const initiative = Math.floor(Math.random() * 20) + 1 + Number(monster.dex);
      this.monsters.push({
        ...monster,
        initiative,
        id,
        type: 'monster',
      });
    },
  },
};
</script>
