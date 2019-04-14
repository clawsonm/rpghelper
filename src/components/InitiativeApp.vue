<template>
  <div class="main-container">
    <div class="sidebar">
      <h2 class="heading">Players</h2>
      <button @click="clearPlayers" class="btnLink">Clear All</button>
      <PlayerList :players="players" @remove-player="onRemovePlayer" />
      <PlayerInput @add-player="onAddPlayer" />
      <h2 class="heading">Monsters</h2>
      <button @click="clearMonsters" class="btnLink">Clear All</button>
      <MonsterList :monsters="monsters" @remove-monster="onRemoveMonster" />
      <MonsterInput @add-monster="onAddMonster" />
    </div>
    <Encounter :players="players" :monsters="monsters" />
  </div>
</template>

<script>
import PlayerList from './PlayerList.vue';
import PlayerInput from './PlayerInput.vue';
import MonsterList from './MonsterList.vue';
import MonsterInput from './MonsterInput.vue';
import Encounter from './Encounter.vue';

export default {
  name: 'InitiativeApp',
  data() {
    return {
      players: [],
      monsters: [],
      lastSave: Date.now(),
    };
  },
  components: {
    PlayerList,
    PlayerInput,
    MonsterList,
    MonsterInput,
    Encounter,
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
    onRemovePlayer(id) {
      this.players = this.players.filter(player => player.id !== id);
    },
    onRemoveMonster(id) {
      this.monsters = this.monsters.filter(monster => monster.id !== id);
    },
    clearMonsters() {
      this.monsters = [];
      localStorage.removeItem('monsters');
    },
    clearPlayers() {
      this.players = [];
      localStorage.removeItem('players');
    },
    persist() {
      if (this.lastSave < Date.now() - 5000) {
        localStorage.setItem('players', JSON.stringify(this.players));
        localStorage.setItem('monsters', JSON.stringify(this.monsters));
      }
    },
  },
  mounted() {
    const players = localStorage.getItem('players');
    if (players) {
      try {
        this.players = JSON.parse(players);
      } catch (e) {
        localStorage.removeItem('players');
      }
    }
    const monsters = localStorage.getItem('monsters');
    if (monsters) {
      try {
        this.monsters = JSON.parse(monsters);
      } catch (e) {
        localStorage.removeItem('monsters');
      }
    }
  },
  watch: {
    players() {
      this.persist();
    },
    monsters() {
      this.persist();
    },
  },
};
</script>

<style scoped>
.heading {
  margin-bottom: 5px;
}
.main-container {
  display: flex;
}
.sidebar {
  height: 100%;
  width: 33%;
  border-right: 3px solid teal;
  padding: 20px;
}
.btnLink {
  background: none;
  color: teal;
  border: none;
  padding: 0;
  cursor: pointer;
}
</style>
