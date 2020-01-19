<template lang="html">
  <section>
    <form v-on:submit.prevent>
      <label for="levelSelect">Please select desired item level:</label>
      <select name="levelSelect" v-model="selectedLevel">
        <option disable value></option>
        <option  v-for="level in itemLevelRange" :value="level">{{ level }}</option>
      </select>
    </form>
  </section>

</template>

<script>
import { eventBus } from '../main.js';

export default {
  name: 'item-level-select',
  data: function () {
    return {
      itemLevelRange: [...Array(100).keys()],
      selectedLevel: null
    }
  },
  watch: {
    selectedLevel: function() {
      eventBus.$emit('level-selected', this.selectedLevel)
    }
  }
}
</script>

<style lang="css" scoped>
</style>
