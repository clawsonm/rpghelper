<template>
  <ul class="initiative">
    <li v-for="char in participants" v-bind:key="char.type + char.id">
      <div class="name">
        {{ char.name }}
      </div>
      <div class="initiative">
        {{ char.initiative }}
      </div>
      <div class="turn-type">
        <em v-if="char.type + char.id === current">current</em>
      </div>
    </li>
  </ul>
</template>

<script>
export default {
  props: ['participants', 'current'],
};
</script>

<style scoped>
  .initiative {
    padding-left: 0;
    /* width: 200px; */
  }
  li {
    display: inline-flex;
    align-items: center;
    justify-content: space-around;
    list-style: none;
    width: 80%;
  }
  .name {
    flex-basis: 30%;
  }
  .turn-type {
    min-width: 60px;
  }
</style>
