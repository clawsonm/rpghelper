<template>
  <ul class="monsters" v-if="monsters.length">
    <li v-for="monster in monsters"
        is="Monster"
        :monster="monster"
        :key="monster.id"
        @click-remove-monster="$emit('remove-monster', monster.id)">
    </li>
  </ul>
</template>

<script>
import Monster from './Monster.vue';

export default {
  name: 'MonsterList',
  props: ['monsters'],
  components: {
    Monster,
  },
};
</script>

<style scoped>
.monsters {
  padding-left: 0;
}
</style>
