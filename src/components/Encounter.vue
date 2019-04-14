<template>
  <div class="encounter">
    <h2 class="heading">Initiative Order</h2>
    <button class="btnLink" @click="onCopyInitiative">Copy</button>
    <EncounterParticipants :participants="sortedPlayersAndMonsters" :current="this.current" />
    <button @click="onNextParticipant">Next</button>
  </div>
</template>

<script>
import EncounterParticipants from './EncounterParticipants.vue';

export default {
  props: ['players', 'monsters'],
  data() {
    return {
      current: '',
    };
  },
  components: {
    EncounterParticipants,
  },
  methods: {
    onNextParticipant() {
      if (this.current === '') {
        this.current = this.sortedPlayersAndMonsters[0].type + this.sortedPlayersAndMonsters[0].id;
      } else {
        const currentIndex = this.sortedPlayersAndMonsters.findIndex(
          participant => participant.type + participant.id === this.current,
        );
        const nextIndex = currentIndex === -1 ? 0
          : (currentIndex + 1) % this.sortedPlayersAndMonsters.length;
        this.current = this.sortedPlayersAndMonsters[nextIndex].type
                        + this.sortedPlayersAndMonsters[nextIndex].id;
      }
    },
    onCopyInitiative() {
      const initiativeString = this.sortedPlayersAndMonsters.reduce((acc, current) => `${acc}${current.name}\t${current.initiative}\n`, 'Initiative\n');
      // eslint-disable-next-line
      navigator.clipboard.writeText(initiativeString).catch(e => console.log(e));
    },
  },
  computed: {
    sortedPlayersAndMonsters() {
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

<style lang="css" scoped>
.heading {
  margin-bottom: 5px;
}
.encounter {
  padding-left: 60px;
}
.btnLink {
  background: none;
  color: teal;
  border: none;
  padding: 0;
  cursor: pointer;
}
</style>
