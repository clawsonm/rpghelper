<template>
  <li>
    <div class="name">
      {{ monster.name }}
    </div>
    <div class="dex">
      <strong>Dex</strong>&nbsp;{{ monster.dex }}
    </div>
    <div class="initiative">
      <strong>Initiative</strong>&nbsp;{{ monster.initiative }}
    </div>
    <button @click="$emit('click-remove-monster')">X</button>
  </li>
</template>

<script>
export default {
  props: ['monster'],
};
</script>

<style scoped>
li {
  display: inline-flex;
  align-content: center;
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
</style>
