<template>
  <ul class="monsters" v-if="monsters.length">
    <li v-for="monster in monsters"
        is="Monster"
        v-bind:monster="monster"
        v-bind:key="monster.id">
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
