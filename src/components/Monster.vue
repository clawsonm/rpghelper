<template>
  <div>
    {{ monster.name }}
    Dex: {{ monster.dex }},
    Initiative: {{ monster.initiative }}
  </div>
</template>

<script>
export default {
  props: ['monster'],
};
</script>

<style scoped>

</style>
