<template lang="html">
  <section>
    <label for="levelSelect">Please select desired item level:</label>
    <select name="levelSelect">
      <option disable value></option>
      <option  v-for="level in itemLevelRange"  v-model="selectedLevel">{{ level }}</option>
    </select>
  </section>

</template>

<script>
import { eventBus } from '../main.js';

export default {
  name: 'item-level-select',
  data: function () {
    return {
      itemLevelRange: [...Array(100).keys()],
      selectedLevel: 0
    }
  },
  watch: {
    selectedLevel: function() {
      eventBus.$emit('level-selected', level)
    }
  }
}
</script>

<style lang="css" scoped>
</style>
